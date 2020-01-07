FROM node:10-slim

LABEL maintainer="Flyerapp"
LABEL info="nodejs base build with knex,yarn and build essential"
LABEL NodeVersion="v10.8.0"

USER root

RUN mkdir -p /opt/apps
RUN chown node:node /opt/apps -R
WORKDIR /opt/apps

# Install node-gyp with dependenies

RUN apt-get update && apt-get install -y libfontconfig git openssh-client curl wget tar bzip2 zip make g++ gcc python build-essential python libfontconfig1 libfontconfig1-dev libfreetype6 libfreetype6-dev chrpath libssl-dev libxft-dev git openssh-client && npm install -g node-gyp  && npm cache clean --force && rm -rf /var/lib/apt/lists/*

# Installing the npm global
RUN  npm i -g yarn react-scripts react-app-rewired knex knex-migrate && npm cache clean --force

