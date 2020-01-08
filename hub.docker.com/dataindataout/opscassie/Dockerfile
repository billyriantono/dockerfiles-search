FROM ubuntu:18.04

LABEL maintainer="Valerie Parham-Thompson" 
LABEL contact="valerie@tortugatech.com" 
LABEL version="2019-11"

ENV LC_ALL C.UTF-8
ENV LANG C.UTF-8

RUN apt-get update \
  && apt-get install -y \
  build-essential \
  git \
  curl \
  wget \
  vim \
  net-tools \
  iputils-ping \
  dnsutils \
  zip \
  unzip \
  ansible \
  libpq-dev python-dev libxml2-dev libxslt1-dev libldap2-dev libsasl2-dev libffi-dev \
  python3-dev python3-pip \
  ant \
  default-jre \
  && apt-get clean \ 
  && rm -rf /var/lib/apt/lists/*

RUN pip3 install cassandra-medusa
RUN pip3 install cstar

VOLUME "/mnt/data"
CMD ["/bin/bash"]