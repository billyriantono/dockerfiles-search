FROM ayyazzafar/cordova

LABEL MAINTAINER="Ayyaz Zafar <contact@ayyaz.io>"

ENV IONIC_VERSION 4.6.0

RUN npm i -g --unsafe-perm ionic@${IONIC_VERSION} && \
    ionic --no-interactive config set -g daemon.updates false && \
    rm -rf /var/lib/apt/lists/* && apt-get clean
RUN mkdir /root/app
WORKDIR "/root/app"
