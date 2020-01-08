FROM        node:8.16-buster-slim
MAINTAINER  Nikhil Dhandre

ENV         MDCHECKR https://github.com/mike42/mdcheckr/releases/download/v1.2/mdcheckr_1.2-1_all.deb
ENV         HOME /home/node

RUN         apt-get update && \
            npm install -g markdownlint-cli && \
            wget $MDCHECKR && \
            dpkg -i --force-depends mdcheckr_1.2-1_all.deb && \
            apt-get -f -y install && \
            rm -rf mdcheckr_1.2-1_all.deb /var/lib/apt/lists/*

WORKDIR     $HOME
VOLUME      ["$HOME"]
