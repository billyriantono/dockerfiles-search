FROM node:alpine
MAINTAINER Hong-Da, Ke
ENV VERSION='1.2.2'

RUN apk update \
    &&apk add yarn tar gzip\
    && cd /root \
    && wget https://github.com/MCS-Lite/mcs-lite-app/releases/download/v1.2.2/linux.tar.gz \
    && tar zxvf linux.tar.gz \
    && cd 7688

WORKDIR /root/7688
EXPOSE 3000 8000 8888
CMD ["node","server.js"]
