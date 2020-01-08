# https://github.com/jupyter/docker-stacks/blob/master/datascience-notebook/Dockerfile
FROM jupyter/datascience-notebook:cf6258237ff9
USER root
RUN conda update python -y
RUN conda update --all -y
RUN pip install blockdiag tensorflow
USER $NB_USER
