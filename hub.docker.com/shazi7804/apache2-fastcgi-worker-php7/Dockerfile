FROM ubuntu:16.04
MAINTAINER shazi7804 <shazi7804@gmail.com>

ENV PHP_VERSION 7.2

# Add non-free and packages
RUN echo 'deb http://archive.ubuntu.com/ubuntu/ xenial multiverse \n\
deb http://archive.ubuntu.com/ubuntu/ xenial-updates multiverse \n\
deb http://archive.ubuntu.com/ubuntu/ xenial-backports main restricted universe multiverse' >> /etc/apt/sources.list

# Add php ppa
RUN set -ex \
      && apt-get update && apt-get install -y \
           python-software-properties \
           software-properties-common \
           language-pack-en-base \ 
      && export LC_ALL=en_US.UTF-8 \
      && export LANG=en_US.UTF-8 \
      && add-apt-repository ppa:ondrej/php

# Install package
RUN set -ex \
      && DEBIAN_FRONTEND=noninteractive \
      && apt-get update && apt-get install -y \
         curl \
         apache2 libapache2-mod-fastcgi \
         php${PHP_VERSION}-cli \
         php${PHP_VERSION}-common \
         php${PHP_VERSION}-fpm \
         php${PHP_VERSION}-mysql \
         php${PHP_VERSION}-mongodb \
         php${PHP_VERSION}-gd \
         php${PHP_VERSION}-json \
         php${PHP_VERSION}-bcmath \
         php${PHP_VERSION}-mbstring \
         php${PHP_VERSION}-xml \
         php${PHP_VERSION}-xmlrpc \
         php${PHP_VERSION}-zip \
         php${PHP_VERSION}-soap \
         php${PHP_VERSION}-sqlite3 \
         php${PHP_VERSION}-curl \
         php${PHP_VERSION}-opcache \
         php${PHP_VERSION}-readline

# Create fastcgi socket
RUN set -ex \
      && touch /usr/lib/cgi-bin/php7.fcgi \
      && chown www-data:www-data /usr/lib/cgi-bin/php7.fcgi

RUN echo "<IfModule mod_fastcgi.c> \n\
  AddHandler php7.fcgi .php \n\
  Action php7.fcgi /php7.fcgi \n\
  Alias /php7.fcgi /usr/lib/cgi-bin/php7.fcgi \n\
  FastCgiExternalServer /usr/lib/cgi-bin/php7.fcgi -socket /var/run/php/php${PHP_VERSION}-fpm.sock -pass-header Authorization -idle-timeout 360 \n\
  <Directory /usr/lib/cgi-bin> \n\
    Require all granted \n\
  </Directory> \n\
</IfModule> \n\
" > /etc/apache2/mods-available/fastcgi.conf

COPY /conf/vhost.conf /etc/apache2/sites-available/000-default.conf

# Manage modules
RUN set -ex \
      && a2dismod mpm_event \
      && a2enmod mpm_worker actions rewrite fastcgi

# Expose port 80 to the outside
EXPOSE 80

#COPY conf/supervisord.conf /etc/supervisor/conf.d/supervisord.conf
#CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]

COPY /scripts/start.sh /start.sh
CMD ["/start.sh"]
