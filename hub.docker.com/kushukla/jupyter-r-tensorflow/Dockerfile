FROM jupyter/datascience-notebook

LABEL maintainer="Kunal Shukla <shuklakunal@gmail.com>"

USER root

RUN apt-get update && \
    apt-get -y install openjdk-8-jdk && \
    apt-get -y install libgfortran3

RUN conda install --quiet --yes -c r \
    'r-rjava=0.9*' \
    'simplegeneric=0.8*' \
    'tensorflow=1.13*' \
    'keras=2.2*' && \
    conda clean -tipsy && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER

RUN R CMD javareconf -e
