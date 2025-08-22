# Plataforma Educativa y de Investigación JupyterHub - Universidad EIA

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Google Cloud Research Credits](https://img.shields.io/badge/Google%20Cloud-Research%20Credits-orange)](https://cloud.google.com/edu/research)

Este repositorio contiene la documentación técnica y operativa para el despliegue de una 
**plataforma educativa y de investigación en la nube basada en JupyterHub**, orientada al 
fortalecimiento de los procesos de enseñanza, aprendizaje y desarrollo de proyectos en la 
Facultad de Ingeniería y Ciencias Básicas de la Universidad EIA.

Implementada sobre Google Cloud con el respaldo del programa 
**Google Cloud Research Credits (USD $5000)**, esta infraestructura busca brindar acceso 
escalable, equitativo y reproducible a entornos computacionales interactivos en Python, R y Julia 
para estudiantes, docentes e investigadores.

---

## 🚀 Objetivos del proyecto

- Diseñar e implementar una infraestructura educativa en la nube basada en JupyterHub.  
- Proveer entornos de análisis y programación en **Python, R y Julia**, accesibles desde la web.  
- Fortalecer la **docencia** con integración en cursos y capacitación docente.  
- Favorecer la **investigación** con espacios de experimentación colaborativa y reproducible.  
- Impulsar la **extensión** mediante apoyo a semilleros y proyectos con alcance externo.  
- Monitorear y optimizar recursos asegurando sostenibilidad más allá de los créditos iniciales.

---

## 🗂️ Estructura del repositorio

```text
proyecto-jupyterhub-eia/
│
├── docs/                      # Sitio web para GitHub Pages (Markdown)
│   ├── anexos.md              # Anexos técnicos del proyecto
|   ├── index.md               # Inicio y resumen ejecutivo
│   ├── propuesta.md           # Propuesta institucional completa
│   ├── infraestructura.md     # Arquitectura técnica y uso de GCP
│   ├── cronograma.md          # Entregables y fechas
│   ├── equipo.md              # Información del equipo de trabajo
│   └── contacto.md            # Datos de contacto
│
├── scripts/                   # Scripts de instalación/configuración
│   ├── install_jupyterhub.sh
│   └── config_authenticator.py
│
├── notebooks/                # Notebooks de ejemplo para los usuarios
│   ├── ejemplo_python.ipynb
│   ├── ejemplo_r.ipynb
│   └── ejemplo_julia.ipynb
│
├── mkdocs.yml                # Configuración para sitio con MkDocs
├── requirements.txt          # Dependencias mínimas del entorno
├── LICENSE                   # Licencia del repositorio (MIT)
└── README.md                 # Este archivo
```

---

## 🌐 Acceso al sitio web del proyecto

El sitio está disponible en:  
🔗 [https://jasanchev.github.io/proyecto-jupyterhub-eia](https://jasanchev.github.io/proyecto-jupyterhub-eia)

Contiene una versión navegable de toda la documentación.

---

## 📌 Tecnologías utilizadas

- **JupyterHub** (plataforma multiusuario)
- **Python, R, Julia** como lenguajes base
- **Google Cloud Platform** (Compute Engine / GKE / Cloud Storage)
- **MkDocs** con tema Material para documentación web
- **GitHub Pages** para publicación libre y abierta

---

## 👥 Equipo del proyecto

- Jaime Alberto Sánchez Velásquez – Coordinador técnico y académico
- Juan Sebastián Valencia Villa – Coordinador técnico y académico
- Duvan Alberto Gómez Betancur – Coordinador técnico y académico  
- Adriana M. Quinchía Figueroa – Dirección de Investigación, Desarrollo e Innovación

---

## 📂 Propuesta completa

La propuesta detallada con justificación, metodología, entregables y plan de sostenibilidad está disponible en:

👉 [`docs/propuesta.md`](./docs/propuesta.md)

---

## 🧠 Licencia y uso de créditos

Este repositorio se publica bajo licencia MIT. Eres libre de reutilizar, adaptar o extender este proyecto, citando la fuente original.

El proyecto cuenta con el apoyo de **Google Cloud Research Credits (USD $5000)**, otorgados directamente a la Universidad EIA. El uso de estos créditos está sujeto a los términos de servicio de Google Cloud Platform y a las condiciones del programa Google Cloud Research Credits, los cuales establecen que los recursos se destinan exclusivamente a actividades de investigación y docencia.

---

## 📬 Contacto

Si deseas conocer más sobre esta iniciativa o replicarla en tu institución, puedes escribir a:

📧 jaime.sanchez@eia.edu.co
📧 juan.valencia72@eia.edu.co
📧 duvan.gomez36@eia.edu.co
📧 adriana.quinchia@eia.edu.co

---


_Última actualización: agosto de 2025_