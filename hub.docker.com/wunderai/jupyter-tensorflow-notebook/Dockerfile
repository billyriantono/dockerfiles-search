FROM jupyter/tensorflow-notebook:latest

USER root
RUN apt-get update && apt-get install -yq git openssh-client recode && rm -rf /var/lib/apt/lists/*
RUN echo "jovyan ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/notebook

USER 1000
