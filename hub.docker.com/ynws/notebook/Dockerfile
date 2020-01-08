FROM jupyter/datascience-notebook

MAINTAINER ynws

USER jovyan

# vim key
RUN mkdir -p $(jupyter --data-dir)/nbextensions && \
    cd $(jupyter --data-dir)/nbextensions && \
    git clone https://github.com/lambdalisue/jupyter-vim-binding vim_binding && \
    jupyter nbextension enable vim_binding/vim_binding

USER root

# SPTK
RUN apt-get update && apt-get install -y csh
RUN wget http://downloads.sourceforge.net/sp-tk/SPTK-3.9.tar.gz && \
    tar xvzf SPTK-3.9.tar.gz && \
    rm SPTK-3.9.tar.gz && \
    cd SPTK-3.9 && \
    ./configure && \
    make && make install && \
    cd - && rm -rf SPTK-3.9

