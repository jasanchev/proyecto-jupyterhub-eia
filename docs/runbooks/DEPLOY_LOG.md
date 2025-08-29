### Paso 1 — Instalación de herramientas en WSL2
- gcloud instalado: v536.0.1
- kubectl instalado: v1.33.4
- helm instalado: v3.18.6
- Fecha: 2025-08-27

### Paso 2 — Configuración inicial de gcloud
- Autenticación completada con la cuenta: jasanchev@gmail.com
- Proyecto seleccionado: proyecto-jupyterhub-eia
- Región: southamerica-west1
- APIs habilitadas:
  - compute.googleapis.com
  - container.googleapis.com
  - artifactregistry.googleapis.com
- Fecha: 2025-08-27

### Paso 3 — Creación del clúster GKE Autopilot

Comando ejecutado:  
gcloud container clusters create-auto jhub-autopilot \  
  --region=southamerica-west1 \  
  --release-channel=regular  

Evidencia de conexión al clúster:  
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

- **IP global:** 34.107.233.192
- **Namespace creado:** jhub
- **Fecha:** 2025-08-27

