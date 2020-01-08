FROM golang:1.8.4

MAINTAINER Philipp Franke <p.franke@gridx.de>

RUN echo "deb http://emdebian.org/tools/debian/ jessie main" > /etc/apt/sources.list.d/crosstools.list \
        && curl http://emdebian.org/tools/debian/emdebian-toolchain-archive.key | apt-key add - \
        && dpkg --add-architecture armel \
        && apt-get update && apt-get install -y --no-install-recommends \
            crossbuild-essential-armel \
        && rm -rf /var/lib/apt/lists/*
