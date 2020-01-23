# Dockerfile for modified scipy-notebook container.
# Brett Milash, CHPC, University of Utah.
ARG BASE_CONTAINER=jupyter/scipy-notebook
FROM $BASE_CONTAINER

LABEL maintainer="Brett Milash <brett.milash@utah.edu>"

USER root

# Install scp, vi, man
RUN apt-get update && \
    apt-get install -y vim && \
    apt-get install -y openssh-client && \
    apt-get install -y man

USER $NB_UID

# Install rise.
RUN conda install -c conda-forge -y rise && \
    jupyter-nbextension install rise --py --sys-prefix && \
    jupyter-nbextension enable rise --py --sys-prefix

# Install nbgrader.
RUN conda install -c conda-forge -y nbgrader && \
    jupyter nbextension install --sys-prefix --py nbgrader --overwrite && \
    jupyter nbextension enable --sys-prefix --py nbgrader && \
    jupyter serverextension enable --sys-prefix --py nbgrader
