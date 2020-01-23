FROM jupyter/base-notebook:latest
MAINTAINER Aurelio Amerio

USER root

RUN apt-get update &&\
    apt-get install -y wget gnupg dirmngr apt-transport-https ca-certificates &&\
    apt-get clean &&\
    conda update conda -y &&\
    conda update --all &&\
    conda install -c anaconda numpy scipy matplotlib astropy pandas -y &&\
    conda install -c numba numba -y &&\
    conda install -c conda-forge pycamb python-language-server -y &&\
    conda clean --yes --all

#add project path to python path
ENV PYTHONPATH=/opt/project

#set working dir to the project directory
WORKDIR /opt/project
ENV HOME=/opt/project

# set secret token
ENV JUPYTER_TOKEN=4eYoitinuQyPHaxnQr9QNU5eu5GUXqiq6qY4VV

#switch back to not root user
USER $NB_UID
