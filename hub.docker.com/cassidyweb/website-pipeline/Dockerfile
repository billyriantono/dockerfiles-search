FROM debian:stable
MAINTAINER Andrew Cassidy <andrew@cassidyweb.co.uk>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y locales python python3 python-pip python3-pip openssh-client yui-compressor

## Set LOCALE to UTF8
#
RUN echo "en_GB.UTF-8 UTF-8" > /etc/locale.gen && \
    echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen && \
    locale-gen && \
    dpkg-reconfigure locales && \
    /usr/sbin/update-locale LANG=en_GB.UTF-8
ENV LC_ALL en_GB.UTF-8