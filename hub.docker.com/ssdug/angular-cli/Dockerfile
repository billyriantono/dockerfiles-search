FROM node:6

MAINTAINER Carter Barnes "carterabarnes@gmail.com"

ARG BUILD_SRC_DIR="/src"

ENV NPM_CONFIG_LOGLEVEL warn

RUN npm install -g @angular/cli

VOLUME "$BUILD_SRC_DIR/"
WORKDIR $BUILD_SRC_DIR
