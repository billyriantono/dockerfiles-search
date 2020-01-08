FROM swun9/docker-ubuntu-base:latest
MAINTAINER swun9 "swung.cn@gmail.com"
ENV REFRESHED_AT 2015-01-11


RUN \
  add-apt-repository -y ppa:nginx/stable && \
  apt-get -qq update && \
  apt-get install -qqy nginx && \
  rm -rf /var/lib/apt/lists/* && \
  echo "\ndaemon off;" >> /etc/nginx/nginx.conf && \
  chown -R www-data:www-data /var/lib/nginx


VOLUME ["/etc/nginx/sites-enabled", "/etc/nginx/certs", "/etc/nginx/conf.d", "/var/log/nginx", "/var/www/html"]

# Define working directory.
WORKDIR /etc/nginx

# Define default command.
CMD ["nginx"]

# Expose ports.
EXPOSE 80
EXPOSE 443
