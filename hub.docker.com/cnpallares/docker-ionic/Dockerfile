FROM cnpallares/docker-cordova

LABEL Carles Albert Pallares <carlesalbert.pallares@gmail.com>

ENV IONIC_VERSION 3.18.0

RUN apt-get update && apt-get install -y git && \
    npm i -g --unsafe-perm ionic@${IONIC_VERSION} && \
    ionic --no-interactive config set -g daemon.updates false && \
    rm -rf /var/lib/apt/lists/* && apt-get clean