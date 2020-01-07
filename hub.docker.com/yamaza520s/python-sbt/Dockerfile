FROM python:3.6-alpine3.6

MAINTAINER Ats Ymzk

# install awscli
RUN pip install --upgrade awscli

# apk update
RUN echo "http://nl.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories \
 && apk update && apk upgrade

# install
RUN apk add openjdk8 \
 && apk add sbt \
 && apk add git \
 && apk add openssh \
 && apk add tar \
 && apk add curl \
 && apk add wget \
 && apk add ca-certificates \
 && apk add docker
