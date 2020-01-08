FROM debian:stable
MAINTAINER Thiago Prado <thiago.gozzi.prado@gmail.com>

RUN apt-get update && apt-get -y install \
  erlang

RUN mkdir -p /workspace
WORKDIR /workspace
VOLUME /workspace

ENTRYPOINT ["erl"]
