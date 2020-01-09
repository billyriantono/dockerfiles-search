FROM ubuntu:14.04

# Some house Keeping stuff
RUN rm /bin/sh && ln -s /bin/bash /bin/sh

RUN apt-get update -y
RUN apt-get install build-essential -y
RUN apt-get install curl -y
RUN apt-get install git -y

# Installing Node & configuring Environment
ENV NVM_DIR /usr/local/nvm
ENV NODE_VERSION_BUILD 5.11.0
ENV NODE_VERSION_DEPLOY 11.1.0
RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.30.2/install.sh | bash \
    && source $NVM_DIR/nvm.sh \
    && nvm install $NODE_VERSION_BUILD \
    && nvm install $NODE_VERSION_DEPLOY \
    && nvm alias default $NODE_VERSION_BUILD \
    && nvm use default
