FROM ubuntu:16.04

MAINTAINER Mike Terzo <mike@terzo.org>

ENV URL="https://pm.puppetlabs.com/cgi-bin/pdk_download.cgi?dist=ubuntu"
ENV VER=1.2.0.0

VOLUME /pdk

RUN apt-get -y update                                                          \
        && apt-get install -y curl                                             \
        && curl -Lo /tmp/pdk.deb "${URL}&rel=16.04&arch=amd64&ver=${VER}"      \
        && dpkg -i /tmp/pdk.deb                                                \
        && rm -f /tmp/pdk.deb                                                  \
        && rm -rf /var/lib/apt/lists/* 

WORKDIR /pdk
