# Docker image specification for Nginx for Drupal.
#
# VERSION 0.1

FROM nginx:1.9.2
MAINTAINER Aleksi Johansson <aleksi@aleksijohansson.net>

# Add the Bro user to run Nginx with permission to the files.
RUN useradd bro -u 1000 -s /bin/bash --no-create-home

# Copy custom Nginx configuration.
COPY provisioning/conf.d /etc/nginx/conf.d
COPY provisioning/nginx.conf /etc/nginx/nginx.conf
