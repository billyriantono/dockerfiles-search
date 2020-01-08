FROM jupyter/datascience-notebook

LABEL maintainer="shunkin <shunkin@west.sd.keio.ac.jp>"

# Schema: https://github.com/projectatomic/ContainerApplicationGenericLabels
LABEL name="Jupyterlab IP analisys environment" \
      summary="The container of jupyterlab with some extra packages" 

USER root

# Install additional packages
RUN apt update 
RUN apt -y install default-jre

USER $NB_UID
# Install dependencies
COPY ./jupyter_docker.yml /home/jovyan/environment.yml  
RUN conda install anaconda-client
RUN conda env update -f /home/jovyan/environment.yml

# Copy jupyter config file
COPY ./jupyter_notebook_config.py /home/jovyan/.jupyter

