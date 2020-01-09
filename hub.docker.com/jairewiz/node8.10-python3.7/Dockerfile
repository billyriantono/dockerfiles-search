FROM python:3.7

ENV NODE_VERSION=8.10.0
ENV NVM_DIR=/root/.nvm

RUN \
  apt-get update && \
  apt-get install -yqq apt-transport-https
RUN \
  wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.33.2/install.sh | bash && \
  . "$NVM_DIR/nvm.sh" && nvm install ${NODE_VERSION} && \
  . "$NVM_DIR/nvm.sh" && nvm use v${NODE_VERSION} && \
  . "$NVM_DIR/nvm.sh" && nvm alias default v${NODE_VERSION} && \
  #ln -s $NVM_DIR/versions/node/v${NODE_VERSION}/bin/n* /usr/bin/ && \
  pip install -U pip && pip install pipenv && \
  rm -rf /var/lib/apt/lists/*

ENTRYPOINT /bin/bash