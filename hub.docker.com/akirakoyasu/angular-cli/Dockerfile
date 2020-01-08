FROM node:8.11
LABEL maintainer="Akira Koyasu <mail@akirakoyasu.net>"

ARG ANGULAR_CLI_VERSION=6.0.2

RUN yarn global add @angular/cli@${ANGULAR_CLI_VERSION} \
  && ng config --global cli.packageManager yarn
RUN mkdir -p /var/lib/angular \
  && chown node:node /var/lib/angular

USER node
WORKDIR /var/lib/angular
