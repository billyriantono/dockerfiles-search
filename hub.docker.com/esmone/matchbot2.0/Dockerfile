FROM ubuntu:latest
LABEL maintainer="Camamber"

RUN apt-get update && apt-get install curl sudo -y
RUN curl -sL https://deb.nodesource.com/setup_10.x | sudo bash -
RUN sudo apt-get install nodejs -y

COPY . /root
WORKDIR /root

EXPOSE 5000

RUN npm install

ENV INTERVAL=0

ENTRYPOINT node index.js $INTERVAL