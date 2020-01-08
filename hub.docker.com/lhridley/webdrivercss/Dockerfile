FROM node:6.8.0-onbuild
MAINTAINER Lisa Ridley <lhridley@gmail.com>

RUN apt-get update && \
    apt-get install -y graphicsmagick && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN npm link && \
    npm link webdrivercss

CMD node 

