FROM jupyter/datascience-notebook:latest
LABEL maintainer=y4m3 description="Add Japanese fonts and latex packages to jupyter/datascience-notebook"

USER root
RUN apt update && apt install -y \
    fonts-ipaexfont \
    fonts-noto-cjk \
    fonts-noto-cjk-extra \
    fonts-noto-mono \
    fonts-ipaexfont \
    dvipng \
    latexmk

USER $NB_UID
RUN tlmgr init-usertree && \
    tlmgr option repository ftp://tug.org/historic/systems/texlive/2017/tlnet-final && \
    tlmgr install bxjscls zxjatype

RUN pip install jupyterlab_latex && \
    jupyter serverextension enable --sys-prefix jupyterlab_latex && \
    jupyter labextension install @jupyterlab/latex && \
    jupyter labextension update --all
