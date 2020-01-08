FROM ubuntu:16.04
MAINTAINER Floyd Joe<floyd@e8bet.net>

# Keep upstart from complaining
RUN dpkg-divert --local --rename --add /sbin/initctl
RUN ln -sf /bin/true /sbin/initctl
# RUN mkdir /var/run/sshd
RUN mkdir /run/php

# Let the conatiner know that there is no tty
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update
RUN apt-get -y upgrade

# Basic Requirements
RUN apt-get -y install pwgen python-setuptools curl git nano sudo unzip openssh-server openssl
RUN apt-get -y install nginx php7.0-fpm php7.0-mysql vim php7.0-dev

# Wordpress Requirements
RUN apt-get -y install php7.0-xml php7.0-mbstring php7.0-bcmath php7.0-zip php7.0-curl php7.0-gd php7.0-intl php-pear php-imagick php7.0-imap php7.0-mcrypt php-memcache php-apcu php7.0-pspell php7.0-recode php7.0-tidy php7.0-xmlrpc php-redis
RUN pecl install grpc

RUN apt-get clean

# mysql config
# RUN sed -i -e"s/^bind-address\s*=\s*127.0.0.1/explicit_defaults_for_timestamp = true\nbind-address = 0.0.0.0/" /etc/mysql/mysql.conf.d/mysqld.cnf

# nginx config
RUN sed -i -e"s/user\s*www-data;/user lumen www-data;/" /etc/nginx/nginx.conf
RUN sed -i -e"s/keepalive_timeout\s*65/keepalive_timeout 2/" /etc/nginx/nginx.conf
RUN sed -i -e"s/keepalive_timeout 2/keepalive_timeout 2;\n\tclient_max_body_size 100m/" /etc/nginx/nginx.conf
RUN echo "daemon off;" >> /etc/nginx/nginx.conf

# php-fpm config
RUN sed -i -e "s/upload_max_filesize\s*=\s*2M/upload_max_filesize = 100M/g" /etc/php/7.0/fpm/php.ini
RUN sed -i -e "s/;cgi.fix_pathinfo\s*=\s*1/cgi.fix_pathinfo=0/g" /etc/php/7.0/fpm/php.ini
RUN sed -i -e "s/post_max_size\s*=\s*8M/post_max_size = 100M/g" /etc/php/7.0/fpm/php.ini
RUN echo "extension=grpc.so" > /etc/php/7.0/mods-available/grpc.ini
RUN sed -i -e "s/;daemonize\s*=\s*yes/daemonize = no/g" /etc/php/7.0/fpm/php-fpm.conf
RUN sed -i -e "s/;catch_workers_output\s*=\s*yes/catch_workers_output = yes/g" /etc/php/7.0/fpm/pool.d/www.conf
RUN sed 's/\# server_tokens off;/server_tokens off;/' -i /etc/nginx/nginx.conf
# replace # by ; RUN find /etc/php/7.0/mods-available/tmp -name "*.ini" -exec sed -i -re 's/^(\s*)#(.*)/\1;\2/g' {} \;

# nginx site conf
ADD ./nginx-site.conf /etc/nginx/sites-available/default
ADD ./www.conf /etc/php/7.0/fpm/pool.d/www.conf

# Supervisor Config
RUN /usr/bin/easy_install supervisor
RUN /usr/bin/easy_install supervisor-stdout
ADD ./supervisord.conf /etc/supervisord.conf

# Add system user for lumen
RUN useradd -m -d /home/lumen -p $(openssl passwd -1 'lumen') -G root -s /bin/bash lumen \
    && usermod -a -G www-data lumen \
    && usermod -a -G sudo lumen

# Install Wordpress
# ADD http://wordpress.org/latest.tar.gz /usr/share/nginx/latest.tar.gz
# RUN cd /usr/share/nginx/ \
#     && tar xvf latest.tar.gz \
#     && rm latest.tar.gz

RUN mkdir /usr/share/nginx/www && echo "<?php phpinfo(); ?>" > /usr/share/nginx/www/index.php
RUN chown -R lumen:www-data /usr/share/nginx/www \
    && chmod -R 775 /usr/share/nginx/www

# Install composer
ADD https://getcomposer.org/download/1.2.1/composer.phar /tmp/composer.phar
RUN chmod +x /tmp/composer.phar
RUN sudo mv /tmp/composer.phar /usr/local/bin/composer

# Wordpress Initialization and Startup Script
ADD ./start.sh /start.sh
RUN chmod 755 /start.sh

#NETWORK PORTS
# private expose
# EXPOSE 9011
EXPOSE 80

# volume for mysql database and wordpress install
# VOLUME ["/usr/share/nginx/www"]
WORKDIR /usr/share/nginx/www
CMD ["/bin/bash", "/start.sh"]
