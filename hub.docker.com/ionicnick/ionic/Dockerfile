FROM node:lts

# Set CI to true & LANG
ENV CI=1
ENV LANG en_US.UTF-8

# Install desired version of cordova if needed if not comment out
ENV CORDOVA_VERSION 8.1.2
RUN npm i -g cordova@${CORDOVA_VERSION} && \
echo n | cordova -v

# Install the desired version of ionic
ENV IONIC_VERSION 4.10.3
RUN npm i -g ionic@${IONIC_VERSION} && \
    ionic --no-interactive config set -g daemon.updates false && \
    ionic --no-interactive config set -g telemetry false

WORKDIR /usr/src/app
