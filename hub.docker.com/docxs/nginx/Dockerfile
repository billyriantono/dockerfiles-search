########################################################################
# Dockerfile for nginx
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
# Component:
# Author:       pjan vandaele <pjan@pjan.io>
# Scm url:      https://github.com/docxs/docker-nginx
# License:      MIT
########################################################################

# pull base image
FROM docxs/base:latest

# maintainer details
MAINTAINER pjan vandaele "pjan@pjan.io"

# Install nginx
RUN \
  apt-prepare && \
  apt-get install -q -y curl && \
  curl http://nginx.org/keys/nginx_signing.key > nginx_signing.key && \
  apt-key add nginx_signing.key && \
  rm nginx_signing.key && \
  echo "deb http://nginx.org/packages/debian/ wheezy nginx" >> /etc/apt/sources.list && \
  echo "deb-src http://nginx.org/packages/debian/ wheezy nginx" >> /etc/apt/sources.list && \
  apt-get update -q -y && \
  apt-get install -y nginx && \
  apt-get remove --purge -q -y curl && \
  apt-cleanup

# Configure nginx
COPY ./config/etc_nginx_nginx.conf /etc/nginx/nginx.conf

# Mountable directories
VOLUME \
  ["/etc/nginx/sites-enabled", "/etc/nginx/certs", "/etc/nginx/conf.d", "/var/log/nginx", "/var/www/html"]

# Define working directory.
WORKDIR \
  /etc/nginx

# Expose the ports
EXPOSE \
  80 443

COPY ./bin/*  /bin/

# Default command.
CMD \
  /bin/nginx-run
