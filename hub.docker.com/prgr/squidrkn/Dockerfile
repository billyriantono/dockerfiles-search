FROM ubuntu:16.04
MAINTAINER me@prgr.org

ENV SQUID_CACHE_DIR=/var/cache/squid \
    SQUID_LOG_DIR=/var/log/squid \
    SQUID_USER=proxy

RUN \
  apt-get update && \
  apt-get -y upgrade && \
  apt-get install -y perl liburi-encode-perl squid3 rsyslog && \
  rm -rf /var/lib/apt/lists/*
COPY entrypoint.sh /sbin/entrypoint.sh
COPY squid.conf /etc/squid/
COPY rkn-acl /etc/squid/
EXPOSE 3128/tcp
EXPOSE 3129/tcp
ENTRYPOINT ["/sbin/entrypoint.sh"]
