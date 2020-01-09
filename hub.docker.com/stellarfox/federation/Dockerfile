FROM ubuntu:18.04

MAINTAINER Grzegorz Szadkowski <5392918+gszadkow@users.noreply.github.com>

RUN set -e \
    && apt update -y \
    && apt install -y \
       bash \
       wget \
    && wget -O federation-snapshot-linux-amd64.tar.gz https://github.com/stellar/go/releases/download/snapshots/federation-snapshot-linux-amd64.tar.gz \
    && tar xvzf federation-snapshot-linux-amd64.tar.gz \ 
    && mv federation-snapshot-linux-amd64/federation /usr/bin/. \
    && rm -rf federation-snapshot-linux-amd64 federation-snapshot-linux-amd64.tar.gz
