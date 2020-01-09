#
# Nginx Dockerfile
#
# https://github.com/dockerfile/nginx
#

# Pull base image.
FROM ubuntu:16.04

# Install Nginx.
RUN \
  apt-get update && \
  apt-get install -y nginx

# Define default command.
CMD nginx -g 'daemon off;'

# Expose ports.
EXPOSE 80
EXPOSE 443
