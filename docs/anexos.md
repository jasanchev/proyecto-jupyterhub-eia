# Anexos técnicos - Proyecto JupyterHub EIA

Este documento contiene los anexos complementarios a la propuesta técnica del despliegue de JupyterHub en Google Cloud. Aquí se incluirán configuraciones, resultados, evidencia, métricas, pruebas técnicas y referencias.

---

## 📁 Contenido del anexo

- 📌 Detalles del clúster GKE
- 💰 Estimación de costos con créditos de Google Cloud
- 🔒 Configuración de autenticación
- 📊 Monitoreo del uso y rendimiento
- 🧪 Evidencia del despliegue exitoso
- 📷 Capturas de interfaz y pruebas
- 📎 Archivos de configuración relevantes (`config.yaml`, scripts, etc.)

---

## 🧱 Detalles del clúster creado

- Proyecto GCP: `proyecto-jupyterhub-eia`
- Zona: `us-central1-a`
- Tipo de nodo: `e2-standard-2`
- Número de nodos: `3`
- Namespace de JupyterHub: `jhub`
- Helm Chart: `jupyterhub/jupyterhub` versión `1.2.0`

---

## 💰 Estimación de costos (ejemplo base)

| Recurso            | Cantidad | Costo estimado mensual |
|--------------------|----------|-------------------------|
| Nodos GKE          | 3 x e2-standard-2 | USD $45 aprox. c/u   |
| Almacenamiento     | 10 GB por usuario | USD $0.10 por GB     |
| Balanceador de carga | 1        | USD $18 aprox.         |
| Tráfico de red     | Dependiente del uso | Incluido en créditos |

📌 Total mensual estimado: **USD $120–150** (ajustable)

---

## 🔐 Configuración de autenticación

Autenticador usado: `firstuseauthenticator` (los usuarios crean su contraseña al primer login).  
Archivo de configuración: `config.yaml`

---

## 📷 Evidencia de despliegue

### Captura de pods activos
```
kubectl get pods --namespace=jhub
```

### Captura del dashboard de acceso
[Inserta imagen aquí]

### URL pública de acceso (IP externa o dominio):
```
http://<external-ip>:8000
```

---

## 📦 Archivos técnicos incluidos

- `config.yaml` – configuración de Helm
- `install_jupyterhub.sh` – script de instalación
- `requirements.txt` – dependencias

---

## 📝 Notas

- Este archivo debe actualizarse a medida que se despliegan más pruebas.
- Puedes usarlo para reportes técnicos o evidencia de avances institucionales.

---

_Última edición: [pendiente de commit]_
