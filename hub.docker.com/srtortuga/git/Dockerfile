FROM alpine:latest
MAINTAINER Fernando Alvarez <fernandoalvarezgomez@gmail.com>

RUN apk add --no-cache git

ENV HOME /root

VOLUME /root/sandbox
WORKDIR /root/sandbox

ENTRYPOINT ["/usr/bin/git"]
