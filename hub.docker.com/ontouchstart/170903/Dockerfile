# https://github.com/jupyter/docker-stacks/tree/cf6258237ff90a45dfc8ee964db4daf87a7c00a3/datascience-notebook
FROM jupyter/datascience-notebook:cf6258237ff9
USER root
RUN mkdir /list
RUN apt-get update -y
RUN apt list --installed > /list/apt.log

RUN conda update python -y
RUN conda update --all -y
RUN conda list > /list/conda.log

RUN pip install blockdiag
RUN pip install tensorflow
RUN pip list --format=columns > /list/pip.log

USER $NB_USER
WORKDIR /work
