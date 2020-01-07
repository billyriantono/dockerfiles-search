# Start from a basic Ubuntu image.
FROM ubuntu:14.04
MAINTAINER Michael Skinner <git@mcskinner.com>

# Install NGINX.
RUN apt-get update && \
  apt-get -y upgrade && \
  apt-get -y install nginx

# Tidy the configs a bit. Most importantly: don't run as daemon when inside this container.
RUN sed -i -e "s/keepalive_timeout\s*65/keepalive_timeout 2/" /etc/nginx/nginx.conf && \
  sed -i -e "s/keepalive_timeout 2/keepalive_timeout 2;\n\tclient_max_body_size 100m/" /etc/nginx/nginx.conf && \
  echo "\ndaemon off;" >> /etc/nginx/nginx.conf && \
  chown -R www-data:www-data /var/lib/nginx

# Expose ports for HTTP and HTTPS.
EXPOSE 80
EXPOSE 443

# Spin up nginx by default.
CMD ["nginx"]
