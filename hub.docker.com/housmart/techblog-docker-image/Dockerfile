FROM debian:latest

ENV HUGO_VERSION 0.31

RUN apt-get update && apt-get install -y wget git
WORKDIR /tmp
RUN wget https://github.com/gohugoio/hugo/releases/download/v0.31/hugo_${HUGO_VERSION}_Linux-64bit.tar.gz
RUN tar -xf hugo_${HUGO_VERSION}_Linux-64bit.tar.gz
RUN mv hugo /usr/local/bin
ENV TZ Asia/Tokyo

WORKDIR /techblog
