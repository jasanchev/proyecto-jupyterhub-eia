
# Propuesta Técnica - Plataforma JupyterHub para docencia e investigación – Universidad EIA

**Universidad EIA**  
**Fecha:** 31 de julio de 2025  
**Coordinador del proyecto:** Jaime Alberto Sánchez Velásquez

---

## 1. CONFIDENCIALIDAD

La información suministrada entre Google Cloud Research Credits y la Universidad EIA para desarrollar esta propuesta se considera confidencial. Se solicita que no se divulgue por ningún medio a terceros sin previa autorización de la Universidad EIA. En caso de ejecución, ambas entidades firmarán un documento específico donde se detallen las condiciones técnicas y de uso.

---

## 2. INTRODUCCIÓN

El acceso equitativo y escalable a recursos computacionales es un desafío crítico en la formación moderna de ingenieros y científicos. La enseñanza de lenguajes como Python, R y Julia para análisis de datos, simulación, optimización o aprendizaje automático requiere ambientes interactivos, reproducibles y accesibles.

Se propone el despliegue de una plataforma educativa basada en JupyterHub sobre Google Cloud, orientada al apoyo de la docencia, la investigación y los proyectos estudiantiles en la Facultad de Ingeniería y Ciencias Básicas. Esta infraestructura proporcionará ambientes de trabajo basados en notebooks, con almacenamiento persistente por usuario, control de acceso, monitoreo y capacidad de escalar dinámicamente.

---

## 3. OBJETIVO GENERAL

Diseñar e implementar una infraestructura educativa en la nube, basada en JupyterHub, que proporcione acceso a ambientes interactivos de desarrollo y análisis para estudiantes y docentes de la Universidad EIA, optimizando el uso de créditos de Google Cloud.

---

## 4. OBJETIVOS ESPECÍFICOS

- Implementar un clúster Kubernetes administrado en Google Cloud que hospede JupyterHub.
- Configurar el control de acceso, el almacenamiento persistente y los entornos base con Python, R y Julia.
- Capacitar a los docentes de los programas en el uso de la plataforma.
- Monitorear y optimizar el uso de recursos en función de la demanda académica.
- Garantizar sostenibilidad técnica y operativa del sistema durante 12 meses con un presupuesto máximo de USD 5000.

---

## 5. EQUIPO DE TRABAJO

| Nombre | Institución | Rol en el proyecto | Responsabilidad asignada |
|--------|-------------|--------------------|---------------------------|
| Jaime Alberto Sánchez Velásquez | Universidad EIA | Coordinador del proyecto | Diseño, despliegue técnico, operación y soporte de la plataforma |
| Adriana M. Quinchía Figueroa | Universidad EIA | Dirección I+D | Acompañamiento estratégico y validación de resultados |

---

## 6. DURACIÓN

**1 año** (agosto 2025 – julio 2026)

---

## 7. METODOLOGÍA

El proyecto se desarrollará en cuatro fases:

### Fase 1: Instalación y pruebas iniciales (1 mes)
- Configuración básica de JupyterHub en GCP, autenticación y prueba piloto.

### Fase 2: Prueba piloto con docentes y estudiantes seleccionados (2 meses)
- Recolección de retroalimentación y ajustes de configuración.

### Fase 3: Integración progresiva en cursos académicos (4 meses)
- Formación de docentes y soporte para cursos que integren la plataforma.

### Fase 4: Escalamiento institucional y monitoreo (5 meses)
- Integración con más programas, seguimiento de uso y sostenibilidad.

---

## 8. ENTREGABLES Y CRONOGRAMA

| Entregable | Fecha estimada |
|------------|----------------|
| Infraestructura desplegada y operativa | Mes 1 |
| Informe de prueba piloto con docentes | Mes 3 |
| Documentación técnica y manual de usuario | Mes 6 |
| Capacitación para docentes | Mes 6 |
| Informe de integración en cursos académicos | Mes 10 |
| Informe final de uso, impacto y recomendaciones | Mes 12 |

---

## 9. VALOR Y FORMA DE FINANCIACIÓN

El valor de la propuesta incluye el uso de créditos por **USD $5,000** otorgados por **Google Cloud Research Credits**, con los cuales se implementará una arquitectura sostenible que garantice el funcionamiento continuo de JupyterHub durante 12 meses.

La solución contempla el despliegue sobre **Google Kubernetes Engine (GKE)** bajo un esquema de recursos optimizados, incluyendo autenticación web, almacenamiento persistente por usuario y entornos de programación en **Python**, **R** y **Julia**.

### Forma de uso y asignación de recursos

- Hasta **50 usuarios activos simultáneamente**, más de 100 usuarios registrados.
- Entornos personalizados por curso con bibliotecas científicas y de análisis de datos.
- Almacenamiento individual de hasta **10 GB por usuario** en Cloud Storage.
- Uso de CPU por defecto, con posibilidad de acceso a GPU bajo demanda para proyectos docentes o de investigación.
- Acceso web seguro con autenticación mediante `FirstUseAuthenticator` o `NativeAuthenticator`.
- Infraestructura **autoescalable** para balancear el uso y controlar los costos.

> **Nota técnica:** Se prioriza la sostenibilidad del entorno con recursos compartidos, limitando el uso intensivo de cómputo para deep learning o simulaciones pesadas. El entorno es ideal para cursos de programación, análisis de datos, estadística, optimización y simulación.

---

## 10. TÉRMINOS Y CONDICIONES

- Google Cloud cubre hasta USD 5000 en créditos no renovables.  
- El servidor será monitoreado para asegurar la eficiencia en el consumo de recursos.  
- Los resultados del proyecto podrán ser compartidos en eventos académicos y publicaciones, respetando la política de uso de la Universidad EIA.

---

## 11. PLAN DE SEGUIMIENTO Y JUSTIFICACIÓN PARA SOLICITUD DE AMPLIACIÓN DE CRÉDITOS

**Nombre del proyecto:** Plataforma JupyterHub para docencia e investigación – Universidad EIA  
**ID del proyecto en GCP:** _[coloca aquí tu ID del proyecto]_  
**Duración estimada:** 12 meses  
**Solicitante:** Jaime Sánchez Velásquez – Profesor investigador, Escuela de Ingeniería y Ciencias Básicas, Universidad EIA

### Objetivo del seguimiento

Establecer mecanismos de monitoreo y evaluación del uso de la infraestructura en Google Cloud para garantizar:
- Uso responsable y eficiente de los créditos
- Evidencia del impacto educativo y científico
- Base sólida para solicitar una extensión de créditos si es necesario

### Indicadores clave de seguimiento (KPI)

| Indicador                       | Frecuencia         | Fuente/Herramienta               |
|--------------------------------|--------------------|----------------------------------|
| Créditos consumidos            | Semanal            | Google Cloud Billing Dashboard   |
| Usuarios registrados           | Mensual            | Dashboard de JupyterHub          |
| Usuarios simultáneos           | Semanal            | Logs / métricas de GKE           |
| Cursos integrados              | Trimestral         | Coordinación académica           |
| Tiempo promedio de sesión      | Mensual            | Logs de uso                      |
| Uso de GPU                     | Bajo demanda       | Métricas de facturación          |
| Actividades investigativas     | Trimestral         | Reportes de proyectos            |

### Plan de informes de avance

- **Mes 3:** Informe interno de consumo y pruebas piloto  
- **Mes 6:** Informe de impacto con métricas clave  
- **Mes 6–7:** Envío de solicitud de ampliación si es necesario  
- **Mes 12:** Informe final técnico y académico  

### Justificación para ampliación de créditos

Se solicitará ampliación si:
- Aumenta la demanda institucional
- Se requiere mayor capacidad de cómputo para investigación
- Se logran resultados destacados en la implementación inicial

### Documentos para soporte

- Reportes de uso de créditos y recursos  
- Notebooks ejecutados por docentes y estudiantes  
- Evidencia de impacto académico y de investigación  
- Plan de uso para nuevos créditos  

---

## 12. INFORMACIÓN DE CONTACTO

**Jaime Alberto Sánchez Velásquez**  
Docente – Escuela de Ingeniería y Ciencias Básicas  
Universidad EIA  
Correo: jaime.sanchez@eia.edu.co  

**Adriana M. Quinchía Figueroa**  
Directora de Investigación, Desarrollo e Innovación  
Universidad EIA  
Correo: adriana.quinchia@eia.edu.co  




