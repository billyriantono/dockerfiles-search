FROM debian:stretch

MAINTAINER Fendi D "jatmikofendi@gmail.com"

# Let the container know that there is no tty
ENV DEBIAN_FRONTEND noninteractive

# Install Basic Requirements
RUN apt-get update \
    && apt-get install --no-install-recommends --no-install-suggests -q -y \
    apt-transport-https \
    lsb-release \
	wget \
	procps \
    apt-utils \
    gnupg \
    curl \
    zip \
    unzip \
    python-pip \
    python-setuptools \
    dirmngr \
    git \
    ca-certificates

RUN echo "#!/bin/sh\nexit 0" > /usr/sbin/policy-rc.d

# Add sources for latest  php
RUN apt-key adv --keyserver hkp://pgp.mit.edu:80 --recv-keys 573BFD6B3D8FBC641079A6ABABF5BD827BD9BF62 \
    && wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg \
    && echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list \
    && apt-get update

# Install PHP
RUN apt-get install --no-install-recommends --no-install-suggests -q -y \
    php7.1-fpm php7.1-cli php7.1-dev php7.1-common php7.1-mysql \
    php7.1-json php7.1-opcache php7.1-readline php7.1-mbstring php7.1-curl php7.1-memcached \
    php7.1-imagick php7.1-mcrypt php7.1-sqlite3 php7.1-zip php7.1-pgsql php7.1-intl php7.1-xml php7.1-redis

# install composer 
RUN curl -ksS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer && \
	composer global require "laravel/installer" 
# install laravelCrudDemo
RUN git clone https://github.com/mul14/laravel-crud-demo.git && \
	mkdir -p /var/www && \
	mv laravel-crud-demo /var/www/laravel && \
	chmod -R 755 /var/www/laravel/* && cd /var/www/laravel && \
	chown -R www-data:www-data /var/www/* && \
	composer install && \
	php artisan migrate --seed -n
# Clean up
RUN apt-get clean && rm -rf /var/lib/apt/lists/*
WORKDIR /var/www/laravel

EXPOSE 8000
CMD ["php","artisan","serve", "--host","0.0.0.0"]
