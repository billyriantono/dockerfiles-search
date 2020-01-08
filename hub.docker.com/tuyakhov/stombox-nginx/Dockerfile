#########################################################################
#
# A Stombox nginx container - used by our API
#
# Build with:
#  docker build -t="tuyakhov/stombox-nginx" .
#
# https://hub.docker.com/_/nginx/
#
########################################################################

# Base from official nginx image
FROM nginx

# Add Stombox API config file.
COPY ./nginx.conf /etc/nginx/nginx.conf

# Add the stombox SSL certificate into the container
#RUN mkdir -p /etc/nginx/ssl
#COPY ./st-server.crt /etc/nginx/ssl/
#COPY ./st-server.key /etc/nginx/ssl/

# Expose logs so other containers (e.g. logstash-forwarder) can process them
VOLUME ["/var/log/nginx"]
