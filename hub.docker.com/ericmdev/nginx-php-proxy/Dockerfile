# Debian: NGINX (PHP Proxy)
#
# VERSION 0.0.1

# Pull the base image.
FROM ericmdev/nginx

# Set the author.
MAINTAINER Eric Mugerwa <dev@ericmugerwa.com>

# Set environment variables.
ENV FILES config/

# Remove default configuration files.
RUN rm -rf /etc/nginx/nginx.conf
RUN mv /etc/nginx/conf.d/default.conf /etc/nginx/conf.d/default.conf.disabled

# Add managed nginx configuration files.
ADD ${FILES}nginx.conf /etc/nginx/
ADD ${FILES}php-app.conf /etc/nginx/conf.d/
ADD ${FILES}fastcgi_params /etc/nginx/
ADD ${FILES}php-upstream.conf /etc/nginx/conf.d/upstream.conf

# Remove default directories.
RUN rm -rf /var/www/*
RUN rm -rf /srv/www/*

# Forward request and error logs to docker log collector.
RUN ln -sf /dev/stdout /var/log/nginx/access.log
RUN ln -sf /dev/stderr /var/log/nginx/error.log

# Define mountable directories.
VOLUME ["/etc/nginx", "/var/log/nginx/", "/var/cache/nginx"]

# Listen on http https ports.
EXPOSE 80 443

# Configure the executable.
ENTRYPOINT ["nginx"]

# Define default command.
CMD []