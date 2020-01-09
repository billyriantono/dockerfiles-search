FROM ubuntu:16.04

ENV FTP_PORT 21
ENV FTP_PASSIVE_PORTS_MIN 30000
ENV FTP_PASSIVE_PORTS_MAX 30015

RUN set -xe \
    && apt-get update \
    && apt-get install -y proftpd \
    && rm -rf /var/lib/apt/lists/*

ADD launch /launch
ADD proftpd.conf /etc/proftpd/proftpd.conf

RUN set -xe \
    && chown root:root /etc/proftpd/proftpd.conf \
    && mkdir /ftp \
    && chmod +x /launch

ENTRYPOINT /launch
