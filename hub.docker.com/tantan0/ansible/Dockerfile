FROM alpine:latest

LABEL maintainer="tantan0"


RUN apk add --no-cache ansible openssh-client
RUN ssh-keygen -b 4096 -t rsa -q -N "" -C "ansible" -f /root/.ssh/id_rsa

VOLUME /data
WORKDIR /data
