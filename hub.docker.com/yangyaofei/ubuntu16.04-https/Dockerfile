FROM ubuntu:16.04


RUN apt-get update \
 && apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common \
 && apt-get clean

COPY sources.list /etc/apt/sources.list