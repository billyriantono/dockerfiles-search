FROM node:4.6.2

MAINTAINER kenjiskywalker <Kenji Naito> "kenji@kenjiskywalker.org"

ENV NPM_VERSION 4.0.3
ENV ANGULAR_CLI_VERSION v1.0.0-beta.21
ENV PHANTOM_JS_VERSION 1.9.7-linux-x86_64

RUN npm install -g npm@$NPM_VERSION
RUN npm install -g angular-cli@$ANGULAR_CLI_VERSION

RUN apt-get update
RUN apt-get install -y curl bzip2 libfreetype6 libfontconfig

RUN curl -sSL https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-$PHANTOM_JS_VERSION.tar.bz2 | tar xjC /
RUN ln -s phantomjs-$PHANTOM_JS_VERSION/bin/phantomjs /usr/local/bin/phantomjs
