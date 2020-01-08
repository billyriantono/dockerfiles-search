FROM alpine:latest
MAINTAINER yaasita

RUN apk update && apk add ansible openssh sshpass
RUN mkdir /root/.ssh
ADD config /root/.ssh
