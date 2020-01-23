# Certbot client on jessie
#
FROM python:2.7-slim

MAINTAINER André Fernandes <andre.oliveira@bcb.gov.br>

RUN echo "deb http://ftp.debian.org/debian jessie-backports main" > /etc/apt/sources.list.d/jessie-backports.list && \
    apt-get update && \
    apt-get install -y python-certbot-apache -t jessie-backports && \
    rm -rf ~/.cache /var/cache/apk/* /tmp/* /*.patch

# volumes
VOLUME /etc/letsencrypt /var/lib/letsencrypt

