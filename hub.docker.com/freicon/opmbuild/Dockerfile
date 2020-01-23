FROM ubuntu:16.04
MAINTAINER Frank Hildebrandt <frank@hildebrandt.io>

RUN apt-get update \
 && apt-get install -y make gcc perl libxml2-dev libz-dev \
 && cpan OTRS::OPM::Maker \
 && mkdir -p /build \
 && apt-get remove -y make gcc libxml2-dev libz-dev \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* 

WORKDIR /build

CMD ["/usr/local/bin/opmbuild"]