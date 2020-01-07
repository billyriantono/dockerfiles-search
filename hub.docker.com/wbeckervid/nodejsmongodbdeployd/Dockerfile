FROM mongo:3.6.8-stretch
# is FROM debian:stretch-slim

### Install node

RUN groupadd --gid 1000 node \
  && useradd --uid 1000 --gid node --shell /bin/bash --create-home node

# replace shell with bash so we can source files
RUN rm /bin/sh && ln -s /bin/bash /bin/sh

# update the repository sources list
# and install dependencies

RUN apt-get update \
    && apt-get install -y --no-install-recommends apt-utils \
    && apt-get install -y --no-install-recommends curl \
    && apt-get install -y --no-install-recommends build-essential \
    && apt-get install -y --no-install-recommends udev \
    && apt-get install -y --no-install-recommends git \
    && apt-get install -y --no-install-recommends python \
    && apt-get install -y --no-install-recommends make \
    && apt-get install -y --no-install-recommends g++ \
    && apt-get install -y --no-install-recommends wget \
    && apt-get install -y --no-install-recommends usbutils \
    && apt-get install -y --no-install-recommends nano \
    && apt-get install -y --no-install-recommends cron \
    && apt-get install -y --no-install-recommends sshpass \
    && apt-get install -y --no-install-recommends bluetooth \
    && apt-get install -y --no-install-recommends bluez \
    && apt-get install -y --no-install-recommends libbluetooth-dev \
    && apt-get install -y --no-install-recommends libudev-dev \
    && apt-get install -y --no-install-recommends etherwake \
    && apt-get -y autoclean

# nvm environment variables
ENV NVM_DIR /usr/local/nvm
ENV NODE_VERSION 10.15.0
ENV NODE_ENV 'production'

# install nvm
# https://github.com/creationix/nvm#install-script
RUN curl --silent -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.2/install.sh | bash

# install node and npm
RUN source $NVM_DIR/nvm.sh \
    && nvm install $NODE_VERSION \
    && nvm alias default $NODE_VERSION \
    && nvm use default

# add node and npm to path so the commands are available
ENV NODE_PATH $NVM_DIR/versions/node/v$NODE_VERSION/lib/node_modules
ENV PATH $NVM_DIR/versions/node/v$NODE_VERSION/bin:$PATH
ENV PATH /opt/X11/bin:$PATH

# confirm installation
RUN node -v
RUN npm -v
RUN npm root -g

#
RUN echo "Europe/Berlin" > /etc/timezone
RUN dpkg-reconfigure -f noninteractive tzdata

### setup deployd

COPY ./src /run
RUN chmod +x -R /run \
&&  mkdir -p /config

ENV ADMIN_USER="admin" \
    ADMIN_PWD="changeme" \
    DB_NAME="" \
    DB_USER="user" \
    DB_PWD="changeme"

# install ncu
RUN npm install -g npm-check-updates

# install deployd
RUN npm install -g deployd-cli

# install pm2
RUN npm install -g pm2

# install frontail
RUN npm install -g frontail

RUN mkdir -p /app

EXPOSE 2403

ENTRYPOINT ["/run/entrypoint.sh"]
