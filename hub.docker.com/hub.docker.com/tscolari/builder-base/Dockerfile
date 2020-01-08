# RUBY MACHINE
FROM tscolari/base
MAINTAINER Tiago Scolari <tscolari@gmail.com>

RUN apt-get update && \
    apt-get install -y --force-yes \
                         build-essential \
                         openssl \
                         ca-certificates \
                         git-core \
                         autoconf \
                         libyaml-dev \
                         libgdbm-dev \
                         automake \
                         libtool \
                         curl \
                         libxslt-dev \
                         libxml2-dev \
                         make && \
    apt-get clean -y && \
    apt-get autoremove -y && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
