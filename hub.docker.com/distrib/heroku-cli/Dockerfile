FROM ubuntu:latest

RUN apt-get update && \
    apt-get -y install curl git && \
    curl https://cli-assets.heroku.com/install.sh | sh && \
    rm -rf /var/lib/apt/lists/*
