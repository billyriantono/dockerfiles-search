# Pull base image.
FROM dockerfile/ubuntu

# Patch the proper apt-get sources
ADD assert/sources.list /etc/apt/sources.list

# Install Nginx.
RUN \
  add-apt-repository -y ppa:nginx/stable && \
  apt-key adv --recv-keys --keyserver keyserver.ubuntu.com 16126D3A3E5C1192 && \
  apt-get update && \
  apt-get install -y nginx && \
  rm -rf /var/lib/apt/lists/* && \
  chown -R www-data:www-data /var/lib/nginx

# Define mountable directories.
VOLUME ["/etc/nginx/sites-enabled", "/etc/nginx/conf.d", "/var/log/nginx"]

# Expose ports.
EXPOSE 80
