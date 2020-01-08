FROM ubuntu:xenial

LABEL maintainer="David Carrera del Castillo <eoldavix@gmail.com>" \
      org.label-schema.url="https://github.com/eoldavix/docker-pdk" \
      org.label-schema.name="Puppet Development Kit tool" \
      org.label-schema.license="Apache-2.0"

ENV DEBIAN_FRONTEND=noninteractive

WORKDIR /root

RUN \
  apt-get update && \
  apt-get install -y wget build-essential && \
  wget "https://pm.puppet.com/cgi-bin/pdk_download.cgi?dist=ubuntu&rel=16.04&arch=amd64&ver=latest" -O pdk.deb && \
  dpkg -i /root/*.deb && \
  rm /root/*.deb && \
  apt-get remove --purge -y wget && \
  apt autoremove -y && \
  rm -rf /var/cache/apt/*

VOLUME ["/app"]

WORKDIR /app

ENTRYPOINT ["/usr/local/bin/pdk"]
CMD []
