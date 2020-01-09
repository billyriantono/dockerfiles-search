FROM jupyter/base-notebook

USER root

RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y software-properties-common -y
RUN add-apt-repository ppa:openscad/releases
RUN apt-get install openscad -y
RUN apt-get install build-essential -y
USER $NB_UID

RUN pip install viewscad
RUN jupyter labextension install @jupyter-widgets/jupyterlab-manager
