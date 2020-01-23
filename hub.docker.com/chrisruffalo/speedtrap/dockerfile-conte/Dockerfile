# Ubuntu
#
# Base Docker Image http://dockerfile.github.io/#/ubuntu
# Authoer: Chenmin

FROM chenmins/oracle-jdk8

MAINTAINER Chenmin <cnlll@qq.com>

# Install.
RUN \
  apt-get update && \
  apt-get install -y inetutils-ping net-tools dnsutils supervisor && \
  rm -rf /var/lib/apt/lists/*

COPY supervisor/supervisord.conf /etc/supervisor/supervisord.conf
COPY supervisor/conf.d/supervisord.conf /etc/supervisor/conf.d/supervisord.conf

# Define default command.
CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/supervisord.conf"]
