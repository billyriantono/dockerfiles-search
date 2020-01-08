FROM ubuntu:14.04

RUN apt-get update && \
    apt-get install curl build-essential -y && \
    (curl -sL https://deb.nodesource.com/setup | bash -) && \
    apt-get install nodejs -y && \
    apt-get clean

RUN npm -g install npm@latest
RUN npm -g install bower grunt
