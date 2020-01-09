# ************************************************************************
# Product    : Home information and control
# Date       : 2017-01-16
# Copyright  : Copyright (C) 2016-2017 Kjeholt Engineering. All rights reserved.
# Contact    : dev@kjeholt.se
# Url        : http://www-dev.kjeholt.se
# Licence    : ---
# -------------------------------------------------------------------------
# File       : base-nodejs-image/Dockerfile-x86
# Version    : 1.1.0
# Author     : Bjorn Kjeholt
# *************************************************************************
 
FROM mhart/alpine-node:latest

MAINTAINER Björn Kjeholt <dev@kjeholt.se>

ARG DOCKER_IMAGE_NAME
ARG DOCKER_IMAGE_TAG

ENV DOCKER_BASE_IMAGE_NAME ${DOCKER_IMAGE_NAME:-UnknownName}
ENV DOCKER_BASE_IMAGE_TAG ${DOCKER_IMAGE_TAG:-UnknownRevision}

RUN apk update && \
    apk add vim && \
    apk add curl

RUN mkdir -p /usr/src/app && \
    mkdir -p /usr/src/app/js && \
    mkdir -p /usr/src/app/script
    
WORKDIR /usr/src/app

# Install app dependencies
ONBUILD COPY package.json /usr/src/app/package-original.json
ONBUILD RUN  sed 's/TestWrapper/js\/main/g' package-original.json > package.json && \
             rm -rf node_modules nbproject

ONBUILD RUN npm install

# Bundle app source

ONBUILD COPY js /usr/src/app/js
ONBUILD COPY Scripts /usr/src/app/script

#-------------------------------------------------------------------------
# Expose port number 3000 to be used if applicable for health check status
#-------------------------------------------------------------------------

EXPOSE 3000

#-------------------------------------------------------------------------
# Check for healthy status
#-------------------------------------------------------------------------

ONBUILD HEALTHCHECK CMD curl --fail http://127.0.0.1:3000/ || exit 1

#-------------------------------------------------------------------------
#-------------------------------------------------------------------------

ONBUILD CMD [ "npm", "start" ]
