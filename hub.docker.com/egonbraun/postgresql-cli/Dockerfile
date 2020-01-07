FROM ubuntu:14.04

MAINTAINER egonbraun

ENV DEBIAN_FRONTEND=noninteractive

VOLUME /mnt/data

RUN apt-get update && apt-get install -y \
  postgresql-client \
  python-pip \
  libpq-dev \
  python-dev

RUN pip install pgcli

ENTRYPOINT /bin/bash
