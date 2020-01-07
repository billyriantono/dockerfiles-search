FROM mysql:5.7
MAINTAINER Tuan.Nguyen <ng.nhat.tuan@gmail.com>

RUN apt-get update \
  && apt-get install --no-install-recommends pv \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

