FROM quay.io/jupyter/scipy-notebook:latest

USER root

RUN apt-get update && apt-get install -y \
    glpk-utils \
    coinor-cbc \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

COPY requirements.txt /tmp/requirements.txt

RUN pip install --no-cache-dir -r /tmp/requirements.txt

USER ${NB_UID}
