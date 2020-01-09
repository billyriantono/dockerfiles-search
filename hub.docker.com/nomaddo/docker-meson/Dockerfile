FROM ubuntu:18.04

RUN apt-get -y update \
 && apt-get -y install meson g++ ca-certificates -y --no-install-recommends \
 && apt-get clean && rm -rf /var/lib/apt/lists/*
