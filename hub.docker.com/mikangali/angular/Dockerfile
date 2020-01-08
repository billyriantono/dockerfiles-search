FROM node:8.11.3

MAINTAINER Michael <mike@mikangali.com>

ENV NPM_VERSION=5.6.0 \
  	FIREBASE_TOOL_VERSION=3.17.4 \
    ANGULAR_CLI_VERSION=6.0.8

# Instal npm tools

RUN	npm i -g --unsafe-perm firebase-tools@${FIREBASE_TOOL_VERSION} @angular/cli@${ANGULAR_CLI_VERSION}

WORKDIR "/app"
