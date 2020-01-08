# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.


#########################
#  Base Image creation  #
#########################

# Effectivelly, it's a datascience-notebook/tensorflow notebook hybrid with some
# jupyter nbextensions, XGBoost and a few additional utils

FROM jupyter/datascience-notebook:7a0c7325e470

USER root

RUN conda config --set ssl_verify False

# install some usefull terminal utils
RUN apt-get update --fix-missing -y \
 && apt-get install -y \
 zip \
 pandoc \
 vim \
 tmux \
 fonts-dejavu 

# Install nbextensions and congigurator
RUN pip install jupyter_nbextensions_configurator jupyter_contrib_nbextensions \
 && jupyter contrib nbextension install \
 && jupyter nbextensions_configurator enable

# this is for presentation mode in notebooks
# but does not work in Jupyterlab
RUN conda install -c damianavila82 rise \
 && fix-permissions $CONDA_DIR \
 && fix-permissions /home/$NB_USER


USER $NB_USER

# install xgboost. Unfortunately a simple pip install
# will not work and this gets a layer
RUN git clone --recursive https://github.com/dmlc/xgboost \
 && cd xgboost; make -j4 \
 && pip install xgboost

# Install Tensorflow
RUN conda install --quiet --yes \
    'tensorflow=1.13*' \
    'keras=2.2*' && \
    conda clean --all -f -y && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER

