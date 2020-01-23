FROM elecnix/geocouch:latest

MAINTAINER Nicolas Marchildon nicolas@marchildon.net

ENV DEBIAN_FRONTEND noninteractive

# Install NodeJS, NPM, Grunt
# https://github.com/joyent/node/wiki/installing-node.js-via-package-manager
RUN apt-get install -y curl git && \
  curl -sL https://deb.nodesource.com/setup | bash - && \
  apt-get install -y nodejs && \
  npm install -g grunt-cli

# Install LibreMap server (libremap-api)
COPY . /home/libremap-api
WORKDIR /home/libremap-api
RUN npm install

# Configure libremap-api
RUN cp couch.json.example couch.json && \
  couchdb -b && sleep 20 && \
  grunt push --couch localhost

# Finalize
USER root
EXPOSE 5484 5974 5986

