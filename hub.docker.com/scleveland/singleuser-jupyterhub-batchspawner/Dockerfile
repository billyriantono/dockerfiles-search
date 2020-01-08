# Build as jupyterhub/singleuser
# Run with the DockerSpawner in JupyterHub

ARG BASE_IMAGE=jupyter/base-notebook
FROM $BASE_IMAGE
MAINTAINER Sean Cleveland <seanbc@hawaii.edu)
ENV JUPYTERHUB_VERSION=1.0.0
ADD install_jupyterhub /tmp/install_jupyterhub
ADD batchspawner /batchspawner
ARG JUPYTERHUB_VERSION=master
# install pinned jupyterhub and ensure notebook is installed
RUN python3 /tmp/install_jupyterhub && \
    python3 -m pip install notebook
RUN cd /batchspawner && \
    python3 -m pip install .
