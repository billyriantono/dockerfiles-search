FROM ubuntu:14.04

MAINTAINER egonbraun

ENV DEBIAN_FRONTEND=noninteractive

VOLUME /mnt/data

RUN apt-get update && apt-get install -y \
  mysql-server-5.6 \
  mysql-client-5.6 \
  mysqltuner

ENTRYPOINT /bin/bash
