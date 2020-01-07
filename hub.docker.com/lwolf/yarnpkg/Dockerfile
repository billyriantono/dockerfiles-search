FROM node:7.2-alpine

MAINTAINER Sergey Nuzhdin <ipaq.lw@gmail.com>

ENV VERSION=0.17.9
ENV DATA_DIR="/data"

RUN npm install -g yarn@$VERSION

RUN mkdir $DATA_DIR

WORKDIR $DATA_DIR

VOLUME $DATA_DIR

ENTRYPOINT ["yarn"]
