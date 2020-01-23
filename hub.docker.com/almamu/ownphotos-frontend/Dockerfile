FROM node:13.2.0
MAINTAINER Alexis Maiquez <almamu@almamu.com>

RUN mkdir -p /root/app/
COPY . /root/app/
WORKDIR /root/app/

ENV CLI_WIDTH 80
RUN npm install
RUN npm install -g serve

EXPOSE 3000

ENTRYPOINT ./run.sh
