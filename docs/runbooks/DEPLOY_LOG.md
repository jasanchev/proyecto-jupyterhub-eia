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