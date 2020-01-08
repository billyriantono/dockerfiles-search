FROM postgres:11
MAINTAINER matsuura0831@gmail.com

RUN apt-get update && \
      apt-get install -y postgis && \
      apt-get clean && \
      rm -rf /var/lib/apt/lists/*
