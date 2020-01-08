FROM ubuntu:16.04

LABEL maintainer="Valerie Parham-Thompson" 
LABEL contact="valerie@tortugatech.com" 
LABEL version="2018-05"

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
  python \
  python-pip \
  ant \
  default-jre \
  && apt-get clean \ 
  && rm -rf /var/lib/apt/lists/*

RUN pip install --upgrade pip
RUN pip install psutil cassandra-driver

CMD ["/bin/bash"]