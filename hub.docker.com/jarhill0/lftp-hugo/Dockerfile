FROM ubuntu:latest

RUN apt-get update \
    && apt-get install -y lftp ssh sshpass \
    && wget https://github.com/gohugoio/hugo/releases/download/v0.58.3/hugo_0.58.3_Linux-64bit.deb \
    && dpkg -i hugo_0.58.3_Linux-64bit.deb \
    && rm -rf /var/lib/apt/lists/*
