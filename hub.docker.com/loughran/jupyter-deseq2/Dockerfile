# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.
FROM jupyter/datascience-notebook:7a3e968dd212
    #2019-07-16 jupyter stack commit
    
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
        bioconductor-deseq2 \
        bioconductor-biomart \
        bioconductor-gage \
        bioconductor-gagedata \
        bioconductor-pathview \
        bioconductor-complexheatmap \
        r-ggbiplot \
    && rm -rf /tmp/* \
    && fix-permissions $CONDA_DIR \
    && fix-permissions /home/$NB_USER

RUN conda install -y -c conda-forge \
        r-pheatmap \
        r-rtsne \
        jupytext \
    && rm -rf /tmp/* \
    && fix-permissions $CONDA_DIR \
    && fix-permissions /home/$NB_USER

RUN Rscript <(echo "install.packages('BiocManager', repos='https://cloud.r-project.org', clean=TRUE)") \
    && Rscript <(echo "BiocManager::install('GenomeInfoDbData')") \
    && Rscript <(echo "BiocManager::install('GenomeInfoDb')") \
    && Rscript <(echo "BiocManager::install('recount')") \
    && Rscript <(echo "install.packages('PoiClaClu', repos='https://cloud.r-project.org', clean=TRUE)") \
    && Rscript <(echo "install.packages('dendextend', repos='https://cloud.r-project.org', clean=TRUE)") \
    && Rscript <(echo "install.packages('tictoc', repos='https://cloud.r-project.org', clean=TRUE)") \
    && rm -rf /tmp/* \
    && fix-permissions $CONDA_DIR \
    && fix-permissions /home/$NB_USER
