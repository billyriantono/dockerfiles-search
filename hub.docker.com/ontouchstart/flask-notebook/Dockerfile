# https://github.com/jupyter/docker-stacks/tree/master/base-notebook
FROM jupyter/base-notebook:bb222f49222e
USER root
RUN conda update python -y
RUN conda update --all -y
RUN conda install -y flask
USER $NB_USER
