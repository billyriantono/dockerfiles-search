FROM ubuntu:16.04

RUN apt-get update \
    && apt-get install -y \
    graphicsmagick \
    curl \
    gnupg \
    && curl -sL https://deb.nodesource.com/setup_6.x | bash - \
    && apt-get install -y nodejs \
    && npm install -g grunt-cli \
    && npm install -g sass

