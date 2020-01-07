FROM node:carbon

## enable sudo
RUN apt-get update && apt-get install -y sudo \
    && adduser node sudo \
    && echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers \
    && apt-get clean && rm -rf /var/lib/apt/lists/

## install jq
RUN apt-get update && apt-get install -y jq \
    && apt-get clean && rm -rf /var/lib/apt/lists/

## set user to avoid permission issues
## (see https://github.com/nodejs/node-gyp/issues/1236)
USER node
RUN mkdir /home/node/.npm-global
ENV PATH=/home/node/.npm-global/bin:$PATH
ENV NPM_CONFIG_PREFIX=/home/node/.npm-global

## install Firebase CLI
RUN npm install -g firebase-tools
