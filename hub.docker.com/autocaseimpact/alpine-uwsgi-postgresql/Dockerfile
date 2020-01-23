FROM ubuntu:trusty
MAINTAINER Tony Hsu
ENV DEBIAN_FRONTEND noninteractive

# add NGINX official stable repository
RUN echo "deb http://ppa.launchpad.net/nginx/stable/ubuntu `lsb_release -cs` main" > /etc/apt/sources.list.d/nginx.list

# add PHP5.6 unofficial repository (https://launchpad.net/~ondrej/+archive/ubuntu/php)
RUN echo "deb http://ppa.launchpad.net/ondrej/php/ubuntu `lsb_release -cs` main" > /etc/apt/sources.list.d/php.list

# install packages
RUN apt-get update && \
    apt-get -y --force-yes --no-install-recommends install \
    supervisor \
    nginx \
    memcached \
    php5.6-cli php5.6-fpm php5.6-common php5.6-mysql php5.6-memcache \
    php5.6-pgsql php5.6-curl php5.6-zip php5.6-gd php5.6-cli \
    php5.6-mcrypt php5.6-opcache php5.6-json php5.6-bz2 php5.6-mbstring \
    wget openssl curl nginx-extras


# configure NGINX as non-daemon
RUN echo "daemon off;" >> /etc/nginx/nginx.conf

# configure php-fpm as non-daemon
RUN sed -i -e "s/;daemonize\s*=\s*yes/daemonize = no/g" /etc/php/5.6/fpm/php-fpm.conf
# clear apt cache and remove unnecessary packages
RUN apt-get autoclean && apt-get -y autoremove
# NGINX mountable directories for config and logs
VOLUME ["/etc/nginx/","/etc/php/", "/var/log/nginx"]
# NGINX mountable directory for apps
VOLUME ["/var/www"]

WORKDIR /var/www/html

# php-fpm5.6 will not start if this directory does not exist
RUN mkdir /run/php
#Time
ENV TW=Asia/Taipei
RUN ln -snf /usr/share/zoneinfo/$TW /etc/localtime && echo $TW > /etc/timezone

RUN mkdir -p /var/www/html && chown -R www-data.www-data /var/www/html

# Append "daemon off;" to the beginning of the configuration
RUN echo "daemon off;" >> /etc/nginx/nginx.conf

RUN ln -sf /dev/stdout /var/log/nginx/access.log \
&& ln -sf /dev/stderr /var/log/nginx/error.log

RUN ln -s /var/www/html /root/www
