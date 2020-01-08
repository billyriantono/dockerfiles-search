FROM node:latest
RUN apt-get update && \
    apt-get -y install rsync apt-utils && \
    apt-get -y remove apt-utils && \
    apt-get -y autoremove && \
    rm -rf /var/lib/apt/lists/*

RUN mkdir -p ~/.ssh && chmod 0700 ~/.ssh
WORKDIR /root/app
