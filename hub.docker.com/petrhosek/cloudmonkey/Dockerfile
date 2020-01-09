# vim:set ft=dockerfile:
FROM debian:wheezy
MAINTAINER Petr Hosek petrhosek@gmail.com

RUN groupadd -r cloudmonkey && useradd -r -m -g cloudmonkey cloudmonkey

RUN apt-get update && apt-get install -y python python-pip

ENV CLOUDMONKEY_VERSION 5.2.0

RUN pip install cloudmonkey==$CLOUDMONKEY_VERSION

RUN mkdir -p /data && chown -R cloudmonkey /data
VOLUME /data

USER cloudmonkey

ENTRYPOINT ["cloudmonkey", "-c", "/data/config"]
