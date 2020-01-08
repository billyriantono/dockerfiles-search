# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.
FROM jupyter/datascience-notebook:1386e2046833
    #2019-09-11 jupyter stack
    #R 3.6.1

LABEL maintainer="jfx319 <jfx319@virginia.edu>"

USER root

#https://docs.docker.com/engine/reference/builder/#shell
SHELL ["/bin/bash", "-c"]

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        fonts-dejavu \
        tzdata \
        gfortran \
        gcc \
        bsdmainutils \
        tree \
        less \
        vim \
        screen \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

USER $NB_UID

RUN conda install -y -c bioconda \
        bioconductor-maftools \
    && rm -rf /tmp/* \
    && fix-permissions $CONDA_DIR \
    && fix-permissions /home/$NB_USER

RUN conda install -y -c conda-forge \
        r-ggpubr \
        r-pheatmap \
        r-gridbase \
        r-gridsvg \
        r-gridextra \
        r-lattice \
        r-desctools \
        r-dt \
        jupytext \
        hide_code \
    && rm -rf /tmp/* \
    && fix-permissions $CONDA_DIR \
    && fix-permissions /home/$NB_USER

RUN Rscript <(echo "install.packages('BiocManager', repos='https://cloud.r-project.org', clean=TRUE)") \
    && Rscript <(echo "install.packages('tictoc', repos='https://cloud.r-project.org', clean=TRUE)") \
    && Rscript <(echo "install.packages('mclust', repos='https://cloud.r-project.org', clean=TRUE)") \
    && Rscript <(echo "BiocManager::install('maftools', update=FALSE)") \
    && rm -rf /tmp/* \
    && fix-permissions $CONDA_DIR \
    && fix-permissions /home/$NB_USER
