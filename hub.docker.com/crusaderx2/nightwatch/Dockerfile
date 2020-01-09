FROM ubuntu:16.04

LABEL mainteiner="thepliable2@gmail.com"

ENV DEBIAN_FRONTEND=noninteractive

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

RUN apt-get update && \
    apt-get install curl=7.47.0-1ubuntu2.14 ca-certificates=20170717~16.04.2 \
    xvfb=2:1.18.4-0ubuntu0.8 -yqq --no-install-recommends && \
    curl -sL https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - && \
    curl -sL https://deb.nodesource.com/setup_12.x | bash - && \
    echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list && \
    apt-get update && \
    apt-get install google-chrome-stable=79.0.3945.79-1 nodejs=12.13.1-1nodesource1 -yqq --no-install-recommends && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /home/nightwatch