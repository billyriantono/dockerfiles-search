FROM continuumio/anaconda3:5.3.0
MAINTAINER kraus1049

COPY ./numpy-site.cfg ~/.numpy-site.cfg

RUN rm -rf ~/.cache/matplotlib && \
    apt-get update && apt-get install -y fonts-ipa* git ssh && apt-get autoremove && \
    fc-cache && \
    ldconfig && \
    git clone -b develop https://fec1d7246bc38dbb90422f2f9ff28c11f8f68e50:x-oauth-basic@github.com/kraus1049/opt_sim /opt/conda/lib/python3.7/site-packages/opt_sim

RUN conda install -c conda-forge nodejs opencv && \
    conda update jupyter jupyterlab && \
    jupyter labextension install jupyterlab_vim && \
    mkdir -p /home/jovyan/libs/ && \
    mkdir /home/jovyan/current_dir && \
    conda update scipy numpy
