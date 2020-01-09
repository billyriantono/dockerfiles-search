FROM ubuntu:trusty
MAINTAINER Arvid van den Brink

RUN apt-get update -q && apt-get install -qy --no-install-recommends \
            texlive-full \
            gnuplot \
            build-essential \
            git \
    &&  rm -rf /var/lib/apt/lists/*

WORKDIR /data
VOLUME ["/data"]