FROM ubuntu:14.04
MAINTAINER Yasuaki Uechi <uetchy@randompaper.co>

# Configure apt-get
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && apt-get upgrade -y

# Install essentials
RUN apt-get install -y \
  build-essential \
  openssl \
  curl \
  git \
  wget \
  vim
