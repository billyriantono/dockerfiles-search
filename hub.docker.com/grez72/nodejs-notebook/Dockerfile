# base-notebook for fmri data analysis in python using nipype
#
# This Dockerfile is based on https://github.com/nipy/workshops/blob/master/170327-nipype/docker/Dockerfile.base,
# which is based on https://github.com/miykael/nipype_env/level0
#
# This means that the same copyrights apply to this Dockerfile, as they do for
# the above mentioned dockerfiles.
#
# pull it:
# docker pull grez72/nodejs-notebook
#
# build it:
# docker build -t grez72/nodejs-notebook https://github.com/grez72/notebooks_test.git#master:nodejs
#
# run it:
# docker run -it --rm -p 8888:8888 grez72/nodejs-notebook
# docker run --user root -it --rm -p 8888:8888 grez72/nodejs-notebook
#-------------------------------------------------------------------------------

FROM jupyter/minimal-notebook
MAINTAINER George Alvarez <grez72@gmail.com, alvarez.wjh.harvard.edu>

USER root
RUN apt-get update
RUN apt-get install libtool pkg-config build-essential autoconf automake -y
RUN apt-get install libzmq-dev -y

WORKDIR /tmp
RUN mkdir -p  $HOME/.ipython/kernels/nodejs
RUN mkdir -p /usr/local/share/jupyter/kernels/
RUN wget https://github.com/notablemind/jupyter-nodejs/releases/download/v1.1.0/jupyter-nodejs-1.1.0.tgz
RUN tar xf jupyter-nodejs-1.1.0.tgz
WORKDIR /tmp/package
RUN npm install && node install.js
RUN cp -R ~/.ipython/kernels/nodejs/ /usr/local/share/jupyter/kernels/

WORKDIR /home/$NB_USER/work
USER $NB_USER
