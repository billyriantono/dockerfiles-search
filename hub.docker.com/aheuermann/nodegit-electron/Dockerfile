FROM node:0.12

MAINTAINER Andrew Heuermann

RUN mkdir /build &&\
  cd /build &&\
  npm init --force &&\
  BUILD_ELECTRON=0.28.1 npm install --save https://github.com/aheuermann/nodegit.git#electron
