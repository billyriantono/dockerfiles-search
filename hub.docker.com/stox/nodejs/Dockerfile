FROM ubuntu:14.04

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

RUN sudo apt-get update && apt-get install -y \
  wget \
  curl \
  libcurl4-openssl-dev \
  unzip

RUN sudo apt-get install -y build-essential python-dev libffi-dev python-pip

RUN sudo apt-get install -y git

ENV NVM_DIR /usr/local/nvm
ENV NODE_VERSION 0.10.30

RUN curl https://raw.githubusercontent.com/creationix/nvm/v0.24.1/install.sh | bash \
    && . $NVM_DIR/nvm.sh \
    && nvm install $NODE_VERSION \
    && nvm alias default $NODE_VERSION \
    && nvm use default

ENV NODE_PATH $NVM_DIR/v$NODE_VERSION/lib/node_modules
ENV PATH      $NVM_DIR/v$NODE_VERSION/bin:$PATH

RUN npm install -g grunt
RUN npm install -g grunt-cli
