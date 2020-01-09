FROM node:8-alpine

WORKDIR /usr/src

COPY python-packages.txt ./

RUN \
  apk --no-cache add bash python py-pip git zip unzip wget && \
  pip install --no-cache-dir -r python-packages.txt && \
  npm install -g jsdoc
