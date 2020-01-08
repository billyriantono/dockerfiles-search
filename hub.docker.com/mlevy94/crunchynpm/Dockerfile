FROM node:alpine

WORKDIR /exec

ADD run.sh /exec

RUN chmod +x run.sh

RUN apk add npm mkvtoolnix rtmpdump ffmpeg bash

RUN npm install -g crunchy

ENV OUTPUT_DIR /data

WORKDIR /config

ENTRYPOINT /exec/run.sh
