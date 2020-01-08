#
# Supervisord & Confd
#
# http://github.com/buddo-io/docker-debian-supervisord

FROM debian:jessie
MAINTAINER lance@buddho.io

ENV DEBIAN_FRONTEND noninteractive

# upgrade system and install Supervisord
RUN apt-get update && apt-get upgrade -y && \
    apt-get install supervisor curl -y && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Install Confd
RUN curl -L https://github.com/kelseyhightower/confd/releases/download/v0.6.3/confd-0.6.3-linux-amd64 -o /usr/local/sbin/confd && \
    chmod 755 /usr/local/sbin/confd

CMD ["/usr/bin/supervisord"]
