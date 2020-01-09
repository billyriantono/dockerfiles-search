FROM ubuntu:bionic-20190807
LABEL maintainer="Chris Kalmar <christian.kalmar@gmail.com>"

ENV SQUID_VERSION=3.5.27 \
    SQUID_CACHE_DIR=/var/spool/squid \
    SQUID_LOG_DIR=/var/log/squid \
    SQUID_USER=proxy

RUN apt-get update \
  && DEBIAN_FRONTEND=noninteractive apt-get install -y squid=${SQUID_VERSION}* \
  && rm -rf /var/lib/apt/lists/*

RUN usermod -a -G tty ${SQUID_USER}

COPY entrypoint.sh /sbin/entrypoint.sh
RUN chmod 755 /sbin/entrypoint.sh

EXPOSE 3128/tcp

ENTRYPOINT ["/sbin/entrypoint.sh"]
