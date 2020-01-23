FROM jupyter/minimal-notebook
USER root
ENV PATH=/home/jovyan/.nimble/bin:$PATH
RUN apt update && \
    apt install -y \
    libczmq-dev \
    curl git && \
    apt clean && \
    rm -rf /var/lib/apt/lists/*

USER $NB_UID

RUN curl https://nim-lang.org/choosenim/init.sh -sSf | sh -s -- -y && \
    nimble refresh && \
    git clone https://github.com/stisa/jupyternim && \
    cd jupyternim && nimble install -y && \
    jupyternim
