FROM debian:8.7
MAINTAINER Alex Pennington <apen525@gmail.com>

## Install core dependencies
RUN apt-get update && apt-get install -y \
    apt-utils \
    bzip2 \
    curl \
    libfontconfig

## Install node
RUN curl -sL https://deb.nodesource.com/setup_7.x | bash -
RUN apt-get update && apt-get install -y \
    nodejs

## Install npm dependencies
RUN npm install -g @angular/cli

ENTRYPOINT npm install \
    && npm cache clean \
    && ng "$@"
