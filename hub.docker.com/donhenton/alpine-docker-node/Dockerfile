# The base docker image is alpine with docker installed
FROM docker:latest

 
RUN apk add --no-cache \
    openssh-client \
    git \
    nodejs \
    py-pip gettext \
    nodejs-npm \
    openssh \
    bash \
    curl wget \
    && pip install docker-compose
 
ENV NODE_VERSION 6.10.3
ENV NPM_VERSION 3.10.10


# You can use these to add ssh keys and scripts
# COPY homedir/ /root
# RUN chmod 400 /root/.ssh/*
# RUN chmod 555 /root/*.sh

 
  