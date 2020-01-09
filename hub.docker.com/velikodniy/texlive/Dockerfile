FROM alpine:3.10
MAINTAINER Vadim Velikodniy <vadim@velikodniy.name>

ENV DIR /tex/
WORKDIR $DIR

RUN apk add --no-cache texlive-full make
RUN apk add --no-cache ghostscript
