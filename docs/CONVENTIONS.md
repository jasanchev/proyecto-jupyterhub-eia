# 📌 Guía de estilos de commit — Proyecto JupyterHub EIA

Esta guía define cómo escribir mensajes de commit claros y consistentes para el proyecto.

## Índice
- [1. Tipos principales](#1-tipos-principales)
- [2. Estructura del mensaje](#2-estructura-del-mensaje)
- [3. Reglas rápidas](#3-reglas-rápidas)
- [4. Ejemplos](#4-ejemplos)
- [📜 Anexo: Ejemplo de historial ideal](#-anexo-ejemplo-de-historial-ideal)

---

## 1. Tipos principales
- **infra:** cambios en infraestructura Kubernetes / GCP / Helm.  
  _Ejemplo:_  
  `infra(config): preparar config.yaml para Ingress GCE + TLS`

- **docs:** cambios en documentación (README, DEPLOY_LOG, propuesta, etc.).  
  _Ejemplo:_  
  `docs(runbook): paso 3 clúster Autopilot creado`

- **chore:** tareas de soporte o mantenimiento (scripts auxiliares, formato, limpieza).  
  _Ejemplo:_  
  `chore: agregar .gitignore y normalizar estructura`

- **feat:** nuevas funcionalidades añadidas al entorno (ej: imagen con R + Julia).  
  _Ejemplo:_  
  `feat(image): añadir soporte Julia en contenedor singleuser`

- **fix:** correcciones de errores de configuración.  
  _Ejemplo:_  
  `fix(config): corregir indentación en config.yaml`

---

## 2. Estructura del mensaje

<tipo>(área): descripción breve en minúsculas

- **tipo**: uno de los definidos arriba.  
- **área**: opcional, indica el archivo o componente (`runbook`, `config`, `helm`, `scripts`).  
- **descripción breve**: qué cambiaste, sin incluir información sensible.  

---

## 3. Reglas rápidas
- ⚠️ **Nunca exponer usuarios, contraseñas ni correos** en los mensajes.  
- ✅ Usar español (coherente con el repo/documentación).  
- 📖 Explicar **qué hiciste** y **para qué**.  
- 🔄 Si un commit afecta docs + infra, puedes dividirlo o escribir ambos (`infra,docs:`).  

---

## 4. Ejemplos
- `infra(config): actualizar config.yaml para despliegue en GKE`  
- `docs(runbook): paso 2 gcloud configurado y APIs habilitadas`  
- `infra(cluster): crear clúster GKE Autopilot`  
- `chore: agregar script bootstrap en WSL2`  
- `fix(config): corregir admin_users no indentado`  

---

## 📜 Anexo: Ejemplo de historial ideal

Así se vería un historial siguiendo esta convención en el proyecto JupyterHub:

```text
commit a1b2c3d (HEAD -> main)
Author: Jaime A. Sánchez <jasanchev@gmail.com>
Date:   2025-08-27

    docs(runbook): paso 3 clúster GKE Autopilot creado

commit 9f8e7d6
Author: Jaime A. Sánchez <jasanchev@gmail.com>
Date:   2025-08-27

    infra(cluster): crear clúster GKE Autopilot en southamerica-west1

commit 7a6b5c4
Author: Jaime A. Sánchez <jasanchev@gmail.com>
Date:   2025-08-27

    docs(runbook): paso 2 gcloud configurado y APIs habilitadas

commit 6543210
Author: Jaime A. Sánchez <jasanchev@gmail.com>
Date:   2025-08-27

    infra(gcloud): configurar proyecto jupyterhub-eia y habilitar APIs

commit 123abcd
Author: Jaime A. Sánchez <jasanchev@gmail.com>
Date:   2025-08-27

    docs(runbook): paso 1 herramientas instaladas en WSL2

commit abc1234
Author: Jaime A. Sánchez <jasanchev@gmail.com>
Date:   2025-08-27

    chore: inicializar repo con documentación base (propuesta, bitácora, anexos)
```