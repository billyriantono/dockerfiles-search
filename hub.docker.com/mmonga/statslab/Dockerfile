FROM jupyter/datascience-notebook
LABEL maintainer="Mattia Monga <mattia.monga@unimi.it>"
USER root
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && apt-get -yq dist-upgrade && apt-get -yq install apt-utils
RUN apt-get -yq install dvipng graphviz libgeos-c1v5 r-base && apt-get clean && rm -rf /var/lib/apt/*
USER $NB_USER
RUN conda install -y -c conda-forge mkl mkl-service theano \
                        jupyter_contrib_nbextensions jupyter_nbextensions_configurator \
                        jupyterlab altair vega_datasets \
                        pymc3 geopandas gdal pysal simplejson \
                        pandas numpy scipy \
                        jupytext && \
                        conda clean -tipsy 
RUN pip install -U --upgrade-strategy eager pystan arviz graphviz
RUN jupyter serverextension enable --py jupyterlab --sys-prefix
RUN jupyter nbextensions_configurator enable --user
USER root
RUN fix-permissions $CONDA_DIR && fix-permissions /home/$NB_USER
USER $NB_USER
