# ------------------------------------------------------------
# IMAGEN BASE: Jupyter Scipy Notebook
# Incluye de fábrica: Python, JupyterLab, Pandas, Numpy, Scipy, Matplotlib
# ------------------------------------------------------------
FROM jupyter/scipy-notebook:2023-10-20
# ------------------------------------------------------------
# INSTALACIÓN COMO ROOT (Para herramientas del sistema)
# ------------------------------------------------------------
USER root
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    git \
    nano \
    htop \
    zip \
    unzip && \
    apt-get clean && rm -rf /var/lib/apt/lists/*
# ------------------------------------------------------------
# VOLVEMOS AL USUARIO "JOVYAN"
# ------------------------------------------------------------
USER ${NB_UID}
# ------------------------------------------------------------
# INSTALACIÓN DE LIBRERÍAS DE PYTHON (curso, sin cambios respecto a v2)
# ------------------------------------------------------------
RUN pip install --no-cache-dir \
    "numpy<2" \
    nbgitpuller \
    openpyxl \
    xlrd \
    statsmodels \
    plotly \
    seaborn \
    tqdm \
    ipywidgets \
    sympy \
    simpy \
    google-cloud-bigquery \
    google-cloud-bigquery-storage \
    pandas-gbq \
    pyarrow \
    db-dtypes

# ------------------------------------------------------------
# LIBRERÍAS NUEVAS — Procesos Estocásticos (Bloque A) y Forecasting (Bloque B)
# ------------------------------------------------------------
RUN pip install --no-cache-dir \
    quantecon \
    networkx \
    pmdarima \
    sktime \
    statsforecast \
    utilsforecast

# ------------------------------------------------------------
# NBGRADER
# ------------------------------------------------------------
RUN pip install --no-cache-dir "nbgrader==0.9.*"

# ------------------------------------------------------------
# Deshabilitado a nivel de imagen; se reactiva solo para el
# perfil de profesor vía lifecycle_hooks en los values de Helm.
# Verificado en vivo: 5 IDs documentados + "menu" (no documentado).
# ------------------------------------------------------------
RUN jupyter labextension disable \
    @jupyter/nbgrader:formgrader \
    @jupyter/nbgrader:assignment-list \
    @jupyter/nbgrader:course-list \
    @jupyter/nbgrader:validate-assignment \
    @jupyter/nbgrader:create-assignment \
    @jupyter/nbgrader:menu && \
    jupyter server extension disable --sys-prefix nbgrader.server_extensions.formgrader

# ------------------------------------------------------------
# HABILITAR EXTENSIONES DE SERVIDOR
# ------------------------------------------------------------
RUN jupyter server extension enable --py nbgitpuller --sys-prefix
