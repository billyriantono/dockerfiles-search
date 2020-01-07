########################################################################
# Dockerfile for RabbitMQ
#
#                    ##        .
#              ## ## ##       ==
#           ## ## ## ##      ===
#       /""""""""""""""""\___/ ===
#  ~~~ {~~ ~~~~ ~~~ ~~~~ ~~ ~ /  ===- ~~~
#       \______ o          __/
#         \    \        __/
#          \____\______/
#
# Component:    RabbitMQ
# Version:      3.3.5-1
# Author:       pjan vandaele <pjan@pjan.io>
# Scm url:      https://github.com/docxs/docker-rabbitmq
# License:      MIT
########################################################################

# Pull base image
FROM \
  docxs/base:latest

# Maintainer details
MAINTAINER \
  pjan vandaele "pjan@pjan.io"

# Install rabbitmq
RUN apt-prepare \
 && echo "deb http://www.rabbitmq.com/debian/ testing main" >> /etc/apt/sources.list \
 && apt-get install -q -y \
      curl \
 && curl http://www.rabbitmq.com/rabbitmq-signing-key-public.asc | apt-key add - \
 && apt-get update -q -y \
 && apt-get install -q -y --no-install-recommends \
      rabbitmq-server \
 && rabbitmq-plugins enable rabbitmq_management \
 && echo "[{rabbit, [{loopback_users, []}]}]." > /etc/rabbitmq/rabbitmq.config \
 && apt-cleanup

# Expose the relevant ports
EXPOSE \
  5672 15672

ENTRYPOINT \
  ["/usr/sbin/rabbitmq-server"]

# docker build [--rm] -t docxs/rabbitmq .
# docker run -h localhost -d -p 5672:5672 -p 15672:15672 docxs/rabbitmq
