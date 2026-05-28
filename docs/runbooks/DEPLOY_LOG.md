### Paso 1 — Preparación del entorno local (WSL2 + herramientas)

**Comandos ejecutados:**  
```bash
wsl --install -d Ubuntu
sudo apt update && sudo apt upgrade -y
bash scripts/wsl2_starter.sh
```
**Evidencia:***
```text
- gcloud instalado: v536.0.1
- kubectl instalado: v1.33.4
- helm instalado: v3.18.6
- Fecha: 2025-08-27
```

### Paso 2 — Configuración inicial de gcloud

**Comandos ejecutados:**
```bash
gcloud auth login
gcloud auth application-default login
gcloud projects list
gcloud config set project <PROJECT_ID>
gcloud config set compute/region southamerica-west1
gcloud services enable compute.googleapis.com
gcloud services enable container.googleapis.com
gcloud services enable artifactregistry.googleapis.com
```
**Evidencia:**

- Autenticación completada con la cuenta: jasanchev@gmail.com
- Proyecto seleccionado: proyecto-jupyterhub-eia
- Región: southamerica-west1
- APIs habilitadas:
  - compute.googleapis.com
  - container.googleapis.com
  - artifactregistry.googleapis.com
- Fecha: 2025-08-27

### Paso 3 — Creación del clúster GKE Autopilot

**Comandos ejecutados:**
```bash  
gcloud container clusters create-auto jhub-autopilot \  
  --region=southamerica-west1 \  
  --release-channel=regular  
gcloud container clusters get-credentials jhub-autopilot --region=southamerica-west1
kubectl cluster-info
kubectl get ns
kubectl get storageclass
```
**Evidencia de conexión al clúster:**

$ gcloud container clusters get-credentials jhub-autopilot --region=southamerica-west1  
Fetching cluster endpoint and auth data.  
kubeconfig entry generated for jhub-autopilot.  

Evidencia de namespaces y cluster-info:  
$ kubectl cluster-info  
Kubernetes control plane is running at https://...  

$ kubectl get ns  
NAME              STATUS   AGE  
default           Active   ...  
kube-system       Active   ...  
gke-managed       Active   ...  

$ kubectl get storageclass  
NAME             PROVISIONER                AGE  
standard-rwo     pd.csi.storage.gke.io      ...  

Observación: En Autopilot es normal que `kubectl get nodes` muestre “No resources found” mientras no haya pods   ejecutándose. El cluster se activa bajo demanda.  

Fecha: 2025-08-27  

### Paso 4 — IP global reservada
**Comandos ejecutados:**
```bash
gcloud compute addresses create jhub-ip --global
gcloud compute addresses describe jhub-ip --global --format="get(address)"
kubectl create namespace jhub
kubectl apply -n jhub -f k8s/jhub-managedcert.yaml
kubectl -n jhub describe managedcertificate jhub-cert
```
**Evidencia:**

- **IP global:** 34.107.233.192
- **Namespace creado:** jhub
- **Fecha:** 2025-08-27

### Paso 5 (prep) — Configuración de JupyterHub lista

Archivo: config.yaml actualizado

- proxy.service: ClusterIP
- ingress.enabled: true (con GCE + IP global + ManagedCert)
- singleuser: imagen quay.io/jupyter/datascience-notebook:latest
- Recursos: 0.5 vCPU / 1–2 GiB RAM
- Autenticación: FirstUseAuthenticator
- admin_users configurado (no se listan los nombres por seguridad)

Fecha: 2025-08-27


### Paso 6 — Pruebas de acceso

Comandos ejecutados:

kubectl -n jhub get ingress
kubectl -n jhub logs deploy/hub


Evidencia:

- Acceso web: https://jupyterhub.eia.edu.co
- Login exitoso con FirstUseAuthenticator


Fecha: YYYY-MM-DD

### Paso 7 — (Opcional) Integración con Google OAuth

Comandos ejecutados:

# credenciales OAuth creadas en GCP
helm upgrade --install jhub jupyterhub/jupyterhub \
  --namespace jhub \
  --values k8s/config-oauth.yaml


Evidencia:

- Autenticación funcionando con cuentas institucionales Google


Fecha: YYYY-MM-DD

### Paso 8 — Perfil GPU: almacenamiento efímero + bucket persistente por investigador (aislamiento IAM)

**Fecha:** 2026-05-27

**Problema que resuelve:**
El perfil GPU usaba un PVC dinámico (pvc_name_template). Los PVC en GKE son
zonales: una vez creado, el pod queda anclado a esa zona. Si esa zona no tenia
GPU L4 disponible, el spawn fallaba con "GCE out of resources", aunque hubiera
capacidad en otras zonas. Solucion: eliminar el PVC del perfil GPU (home
efimero con emptyDir) y dar persistencia mediante una carpeta por investigador
en un bucket GCS, con aislamiento real por IAM (Workload Identity).

**Arquitectura resultante (perfil GPU):**
- /home/jovyan             -> emptyDir (efimero, no ancla zona)
- /home/jovyan/persistente -> carpeta del investigador en gs://jhub-eia-trabajo
- /srv/shared              -> bucket compartido (solo lectura), sin cambios

**1. Bucket de trabajo:**
gcloud storage buckets create gs://jhub-eia-trabajo \
  --project=jupyterhub-eia --location=us-central1 \
  --uniform-bucket-level-access --public-access-prevention
Carpeta por investigador: un objeto marcador <carpeta>/.keep por cada uno.

**2. Identidades por investigador (x6):**
- 1 GSA por investigador: gpu-inv-N@jupyterhub-eia.iam.gserviceaccount.com
- 1 KSA por investigador en namespace jhub: gpu-ksa-<carpeta>
- Workload Identity (dos direcciones):
  - GSA: roles/iam.workloadIdentityUser para
    serviceAccount:jupyterhub-eia.svc.id.goog[jhub/<ksa>]
  - KSA: annotation iam.gke.io/gcp-service-account=<gsa-email>

**3. Permisos sobre buckets:**
- gs://jhub-eia-trabajo: cada GSA con roles/storage.objectAdmin
  CONDICIONADO al prefijo propio:
  resource.name.startsWith('projects/_/buckets/jhub-eia-trabajo/objects/<carpeta>/')
  -> aislamiento de escritura: cada quien solo en su carpeta.
- gs://jhub-eia-trabajo: cada GSA con roles/storage.legacyBucketReader SIN condicion.
  -> CLAVE: gcsfuse necesita storage.objects.list (bucket-level) para montar.
     La condicion de prefijo NO cubre el list (no es operacion sobre objeto),
     asi que el montaje falla con PermissionDenied si falta este rol.
- gs://jhub-eia-shared: cada GSA con roles/storage.objectViewer (solo lectura).

**4. Cambio en values-datahub-prod.yaml (perfil GPU):**
- Eliminado pvc_name_template.
- volumes/volume_mounts como claves DIRECTAS de kubespawner_override
  (reemplazan la lista base del chart, que incluia el PVC global; si se
  ponen dentro de extra_pod_config NO reemplazan y el PVC se cuela).
- service_account = KSA derivada del UPN del usuario.
- only-dir=<carpeta> en gcsfuse -> cada pod solo ve su carpeta.

**5. Validacion (OK):**
CUDA disponible: True | GPU: NVIDIA L4
Benchmark matmul 10000x10000 -> GPU 20.6x mas rapida que CPU
Escritura en /home/jovyan/persistente confirmada en gs://jhub-eia-trabajo/<carpeta>/

**NOTAS OPERATIVAS (importante para mantenimiento):**
- ALTA de un investigador GPU = DOS pasos obligatorios:
  (a) agregar su correo a gpu_users.txt en el ConfigMap (para que vea el perfil)
  (b) crear su GSA + KSA + Workload Identity + condicion IAM + carpeta (Paso 2-3)
  Si falta (b), el pod arranca pero falla al montar el bucket.
- Cuota GPU: NVIDIA_L4_GPUS=16, GPUS_ALL_REGIONS=2 (limite efectivo: 2 GPUs
  simultaneas). La cuota NO es el cuello de botella.
- Cuello de botella real: DISPONIBILIDAD fisica de L4 en us-central1 (intermitente,
  mejor en horario nocturno). No se resuelve con config. Opciones a futuro:
  reservation puntual de capacidad, u otra region.
