FROM debian:stretch-20181011 
# Debian 9.5
MAINTAINER <a38y@myplace.dk>

RUN apt-get update -q \
  && apt-get install -qy \
    deluge-common=1.3.13+git20161130.48cedf63-3 \
  && rm -rf /var/lib/apt/lists/* \
;
