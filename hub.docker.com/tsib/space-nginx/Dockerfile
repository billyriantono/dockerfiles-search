FROM ubuntu:14.04

ENV TERM vt100
RUN usermod -u 1000 www-data

# Install Nginx.
RUN \
  apt-get update && \
  apt-get install -y nginx && \
  apt-get install -y php5-fpm php5-mysql php5-mcrypt php5-curl php5-cli php5-imagick && \
  rm -rf /var/lib/apt/lists/* && \
  echo "\ndaemon off;" >> /etc/nginx/nginx.conf && \
  chown -R www-data:www-data /var/lib/nginx && \
  rm /etc/nginx/sites-available/default

# Enable modules
RUN php5enmod mcrypt && \
    php5enmod imagick && \
    php5enmod curl


# Add config for nginx
ADD /default /etc/nginx/sites-available/
ADD /custom.conf /etc/nginx/conf.d/custom.conf

# Add config to php.ini
RUN \
    echo "cgi.fix_pathinfo=0" >> /etc/php5/fpm/php.ini

# Change ownership
RUN mkdir /var/www && \
    chown -R www-data:www-data /var/www

# Define mountable directories.
VOLUME ["/etc/nginx/sites-enabled", "/etc/nginx/certs", "/etc/nginx/conf.d", "/var/log/nginx", "/var/www"]

# Restart services
CMD service php5-fpm restart && nginx

# Define working directory.
WORKDIR /etc/nginx

# Define default command.
#CMD ["nginx"]

# Expose Ports
EXPOSE 443
EXPOSE 80

