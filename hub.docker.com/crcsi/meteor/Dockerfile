FROM node:4.8.3
MAINTAINER Alex Leith <aleith@crcsi.com.au>

RUN npm cache clean -f && npm install -g n && n 4.8.3

# Attempt to fix builds on Docker Cloud. See: https://github.com/docker/hub-feedback/issues/727
RUN apt-get update && apt-get install -y --no-install-recommends bsdtar
RUN ln -s /usr/bin/bsdtar /usr/local/bin/tar 

ENV METEOR_VERSION 1.5

RUN curl https://install.meteor.com/?release=$METEOR_VERSION | sh

# Unlink the tar replacement
RUN rm -f /usr/local/bin/tar
