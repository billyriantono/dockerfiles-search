FROM debian:stable-slim
LABEL maintainer "Bruno Oliveira <bruno@bono.io>"

RUN     apt-get -qq update && \
        apt-get -qq install -y curl build-essential && \
        curl -sL https://deb.nodesource.com/setup_8.x | bash - && \
        apt-get -qq install -y nodejs && \
        curl https://install.meteor.com/ | sh && \
        useradd -m appuser

WORKDIR /home/appuser

USER appuser

RUN meteor --version