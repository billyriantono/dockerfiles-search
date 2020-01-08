FROM jupyter/datascience-notebook:latest

ARG JUPYTER_ENABLE_LAB=true

LABEL maintainer="Clément Trassoudaine <clement.trassoudaine@eurecom.fr>"
LABEL Author="Clément Trassoudaine"
LABEL Version=0.1

USER $NB_UID

RUN conda install -c conda-forge \
    neo4j-python-driver \
    && conda clean -tipsy

RUN pip install neopylib 

