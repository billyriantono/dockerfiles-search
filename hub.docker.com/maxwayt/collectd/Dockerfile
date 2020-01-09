#
# Dockerfile for collectd
#

FROM debian:jessie
MAINTAINER Max <max@wayt.me>

RUN apt-get update && \
    apt-get install -y --no-install-recommends collectd && \
    rm -rf /var/lib/apt/lists/*

COPY collectd.conf /etc/collectd/collectd.conf
COPY collection.conf /etc/collectd/collection.conf

CMD ["collectd", "-f"]
