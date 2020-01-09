
FROM debian:8.7

# Install system tools
RUN apt-get update \
    && apt-get install -y wget apt-transport-https ca-certificates

# Add nginx and php repositories to apt-get
RUN cd tmp \
    && wget http://nginx.org/keys/nginx_signing.key \
    && apt-key add nginx_signing.key \
    && echo "deb http://nginx.org/packages/debian/ jessie nginx" >> /etc/apt/sources.list \
    && echo "deb-src http://nginx.org/packages/debian/ jessie nginx" >> /etc/apt/sources.list \
    && wget https://www.dotdeb.org/dotdeb.gpg \
    && apt-key add dotdeb.gpg \
    && echo "deb http://packages.dotdeb.org jessie all" >> /etc/apt/sources.list \
    && echo "deb-src http://packages.dotdeb.org jessie all" >> /etc/apt/sources.list \
    && wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg \
    && echo "deb https://packages.sury.org/php/ jessie main" > /etc/apt/sources.list.d/php.list \
    && apt-get update

# Install nginx and configurate id
RUN apt-get install -y nginx
RUN rm -rf /etc/nginx/conf.d/default.conf
ADD config/nginx/nginx.conf /etc/nginx/nginx.conf
ADD config/nginx/php70.conf /etc/nginx/php70.conf
# ADD config/nginx/conf.d /etc/nginx/conf.d

# Install php and configurate id
RUN apt-get install -y php7.1-fpm php7.1-mysql php7.1-curl php7.1-mbstring php7.1-xdebug php7.1-xml php7.1-imagick php7.1-zip
RUN sed -i 's/;daemonize = yes/daemonize = no/g' /etc/php/7.1/fpm/php-fpm.conf
ADD config/php/fpm/pool.d /etc/php/7.1/fpm/pool.d
RUN mkdir /run/php

# Install imagemagick
RUN apt-get install -y imagemagick

# Install supervisor and configurate it
RUN apt-get install -y supervisor
ADD config/supervisor/supervisord.conf /etc/supervisor/supervisord.conf
ADD config/supervisor/conf.d /etc/supervisor/conf.d

EXPOSE 80

ENTRYPOINT supervisord
