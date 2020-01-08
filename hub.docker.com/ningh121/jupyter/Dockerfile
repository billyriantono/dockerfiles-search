FROM jupyter/base-notebook

USER root

RUN apt-get update -y && \
    apt-get install -y gcc-7 && \
    conda install xeus-cling notebook -c QuantStack -c conda-forge -y

USER $NB_UID
