FROM node:latest

RUN apt-get update && \
    apt-get -y install rsync && \
    apt-get -y install unzip && \
    apt-get -y --no-install-recommends install php5-cli && \
    apt-get autoclean && apt-get clean && apt-get autoremove
