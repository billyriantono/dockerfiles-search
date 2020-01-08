FROM node:argon

MAINTAINER Steven <ineva@qq.com>

VOLUME /data
WORKDIR /data

RUN npm install -g local-npm

ENV HOST_IP='127.0.0.1'
ENV HOST_PORT=5080

EXPOSE 5080
EXPOSE 16984

CMD local-npm --url-base http://$(echo $HOST_IP:$HOST_PORT)
