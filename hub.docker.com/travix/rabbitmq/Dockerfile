#
# RabbitMQ Dockerfile
#
# https://bitbucket.org/xivart/docker-rabbitmq
#

# Pull base image
#FROM ubuntu:trusty
# ^ official image has broken `su` because of PAM audit feature
#   The following image has a workaround
FROM sequenceiq/pam:ubuntu-14.04

# Set container author
MAINTAINER Frits Vlaanderen

# Add files
ADD bin/rabbitmq-start /usr/local/bin/
ADD bin/rabbitmq-server /usr/lib/rabbitmq/bin/rabbitmq-server

# Install RabbitMQ
RUN \
  apt-key adv --keyserver keyserver.ubuntu.com --recv-keys F7B8CEA6056E8E56 \
  && echo "deb http://www.rabbitmq.com/debian/ testing main" \
      > /etc/apt/sources.list.d/rabbitmq.list \
  && apt-get update \
  && DEBIAN_FRONTEND=noninteractive apt-get install -y rabbitmq-server \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* \
  && rabbitmq-plugins enable \
      rabbitmq_management \
      rabbitmq_shovel \
      rabbitmq_shovel_management \
      rabbitmq_auth_backend_ldap \
  && echo "[{rabbit, [{loopback_users, []}]}]." \
      > /etc/rabbitmq/rabbitmq.config \
  && chmod +x /usr/local/bin/rabbitmq-start \
  && chmod +x /usr/lib/rabbitmq/bin/rabbitmq-server

# Define environment variables
ENV RABBITMQ_LOG_BASE /data/log
ENV RABBITMQ_MNESIA_BASE /data/mnesia

# Define mountable directories
VOLUME ["/data"]

# Define working directory
WORKDIR /data

# Define default command
CMD ["rabbitmq-start"]

# Expose ports
EXPOSE 5672
EXPOSE 15672
