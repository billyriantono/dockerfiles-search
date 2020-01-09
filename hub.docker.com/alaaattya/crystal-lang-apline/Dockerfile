FROM alpine:3.7

MAINTAINER Alaa Attya <alaa.attya91@gmail.com>

RUN apk add --no-cache gnupg
RUN echo http://public.portalier.com/alpine/testing >> /etc/apk/repositories \
      && wget http://public.portalier.com/alpine/julien%40portalier.com-56dab02e.rsa.pub -O /etc/apk/keys/julien@portalier.com-56dab02e.rsa.pub \
      && apk add --no-cache crystal=0.23.1-r1 shards