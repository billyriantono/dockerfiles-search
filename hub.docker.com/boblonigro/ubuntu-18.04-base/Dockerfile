FROM ubuntu:18.04

RUN apt-get update && apt-get upgrade -y

COPY debconf-preseed.txt /build/debconf-preseed.txt

ENV DEBIAN_FRONTEND=noninteractive
ENV DEBCONF_NONINTERACTIVE_SEEN=true

RUN debconf-set-selections /build/debconf-preseed.txt

RUN apt-get install -y tzdata

RUN apt-get update && apt-get install -y emacs htop r-base-core ess

RUN apt-get update && apt-get install -y python python-pip libxml2-dev libcurl4-openssl-dev libssl-dev libsasl2-dev

COPY install-r-packages.R /build/install-r-packages.R

RUN Rscript /build/install-r-packages.R



