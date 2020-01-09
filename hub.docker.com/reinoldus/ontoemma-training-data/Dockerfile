FROM ubuntu:18.04

RUN apt-get update && apt-get install -y gzip wget git

COPY download-data.sh /

RUN mkdir -p /data && bash download-data.sh

