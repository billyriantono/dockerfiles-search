FROM jupyter/minimal-notebook
MAINTAINER cinos81@gmail.com

USER root
RUN apt-get -qq update
#http://askubuntu.com/questions/365074/cannot-install-zeromq-package-from-chris-lea-zeromq-in-12-04/388770#388770
RUN apt-get install libzmq3-dbg libzmq3-dev libzmq3 -yqq
RUN apt-get install build-essential -yqq
RUN apt-get install curl -yqq

USER $NB_USER
WORKDIR /tmp
RUN git clone https://github.com/notablemind/jupyter-nodejs.git
WORKDIR /tmp/jupyter-nodejs
RUN mkdir -p ~/.ipython/kernels/nodejs/
RUN npm install && node install.js
RUN npm run build
RUN npm run build-ext

WORKDIR /home/$NB_USER/work
