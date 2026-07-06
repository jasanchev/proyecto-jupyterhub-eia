FROM quay.io/jupyter/base-notebook:latest

USER root

RUN apt-get update && apt-get install -y \
    build-essential \
    gcc \
    g++ \
    make \
    cmake \
    git \
    wget \
    curl \
    ca-certificates \
    pkg-config \
    gdb \
    valgrind \
    libxerces-c-dev \
    libexpat1-dev \
    zlib1g-dev \
    libeigen3-dev \
    libx11-dev \
    libxmu-dev \
    libxi-dev \
    libgl1-mesa-dev \
    libglu1-mesa-dev \
    freeglut3-dev \
    qtbase5-dev \
    libqt5opengl5-dev \
    libopenmpi-dev \
    openmpi-bin \
    vim \
    nano \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

RUN mkdir -p /opt/geant4 /opt/geant4/src /opt/geant4/build /opt/geant4/install \
 && chown -R ${NB_UID}:users /opt/geant4

USER ${NB_UID}

RUN echo 'export GEANT4_HOME=/opt/geant4' >> ~/.bashrc && \
    echo 'export PATH=/opt/geant4/install/bin:$PATH' >> ~/.bashrc