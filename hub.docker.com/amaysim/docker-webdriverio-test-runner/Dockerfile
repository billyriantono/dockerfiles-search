FROM node:8-slim

ENV PYTHON=/usr/bin/python2.7 NODE_PATH=/node_modules

COPY package.json ./package.json

RUN apt-get update && \
    apt-get install --no-install-recommends -y \
      g++ build-essential python2.7 zip unzip git && \
    npm install --no-bin-links --quiet --global && \
    npm cache clean --force && \
    rm -rf /var/lib/apt/lists/*