#
# Nginx Dockerfile
#
# https://github.com/dockerfile/nginx
#

# Pull base image.
FROM dockerfile/ubuntu

# Install Nginx.
RUN \
  add-apt-repository -y ppa:nginx/stable && \
  apt-get update && \
  apt-get install -y nginx && \
  rm -rf /var/lib/apt/lists/* && \
  chown -R www-data:www-data /var/lib/nginx

#copy default simple setup
COPY conf/sites-enabled/default /etc/nginx/sites-enabled/default
COPY conf/nginx.conf /etc/nginx/nginx.conf
# Define mountable directories.
VOLUME ["/etc/nginx/sites-enabled", "/etc/nginx/", "/etc/nginx/certs", "/etc/nginx/conf.d", "/var/log/nginx", "/var/www/"]

# Define working directory.
WORKDIR /etc/nginx

# Expose ports.
EXPOSE 80
EXPOSE 8080
EXPOSE 443

# Define default command.
CMD ["nginx"]

