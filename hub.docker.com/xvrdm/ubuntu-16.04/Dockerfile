FROM ubuntu:16.04
MAINTAINER Xavier Adam <xaad@protonmail.com>

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update
RUN apt-get install -y --no-install-recommends \
      apt-utils apt-transport-https
RUN apt-get upgrade -y
RUN apt-get install -y --no-install-recommends \
      software-properties-common build-essential \
      libcurl4-openssl-dev libssl-dev libssh2-1-dev \
      libxml2-dev \
      libcairo2-dev \
      wget vim

ENV DEBIAN_FRONTEND=text
CMD ["echo","hello"]
