FROM ruby:2.3

MAINTAINER Chris Runo <chris.runo@gmail.com>

ENV DEBIAN_FRONTEND noninteractive
ENV LC_ALL=C.UTF-8

RUN DEBIAN_FRONTEND=noninteractive apt-get -y install;

# Replace shell with bash so we can source files and install packages.
RUN rm /bin/sh && ln -s /bin/bash /bin/sh && \
    apt-get update && \
    apt-get -y upgrade; \
    apt-get -y dist-upgrade && \
    apt-get install -y python-software-properties && \
    apt-get install -y software-properties-common && \
    apt-get update --fix-missing;

# Install basic packages
RUN apt-get -y install \
    libssl-dev \
    build-essential \
    rsync;

# Install node and npm
ENV NVM_DIR /usr/local/nvm
ENV NODE_VERSION 7.5.0
RUN curl --silent -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.2/install.sh | bash && \
    source $NVM_DIR/nvm.sh && \
    nvm install $NODE_VERSION && \
    nvm alias default $NODE_VERSION && \
    nvm use default;

# Add node and npm to path so the commands are available
ENV NODE_PATH $NVM_DIR/v$NODE_VERSION/lib/node_modules
ENV PATH $NVM_DIR/versions/node/v$NODE_VERSION/bin:$PATH

# Clean up installs
RUN apt-get clean && apt-get autoremove;

CMD bash
