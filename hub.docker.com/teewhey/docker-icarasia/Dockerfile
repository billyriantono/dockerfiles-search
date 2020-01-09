FROM debian:jessie

MAINTAINER David Chin "teewhey@hotmail.com"

ENV DEBIAN_FRONTEND noninteractive
ENV LANG       en_US.UTF-8
ENV LC_ALL     en_US.UTF-8

# REGISTER DOTDEB REPO
RUN echo "deb http://packages.dotdeb.org jessie all" > /etc/apt/sources.list.d/dotdeb.list && \
echo "deb-src http://packages.dotdeb.org jessie all" >> /etc/apt/sources.list.d/dotdeb.list && \
apt-get -y update && \
apt-get install -y wget sudo && \
wget https://www.dotdeb.org/dotdeb.gpg && \
sudo apt-key add dotdeb.gpg

# INSTALL NEEDED PACKAGES
RUN apt-get -y update && \
apt-get -y install nginx-extras \
	php5 \
	php5-cli \
	php5-common \
	php5-curl \
	php5-mysqlnd \
	php-pear \
	php5-fpm \
	php5-redis \
	php5-memcached \
	php5-mcrypt \
	libapache2-mod-php5 \
	php5-dev \
	php-apc \
	supervisor \
	locales-all \
	apt-utils

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /etc/nginx/sites-enabled/*

ADD ./config/supervisor/supervisor.conf /etc/supervisor/conf.d/supervisord-nginx-fpm.conf
ADD ./config/nginx/nginx-fpm.conf /etc/nginx/sites-enabled/nginx-fpm.conf

RUN usermod -u 1000 www-data && chown -R www-data:www-data /var/www

EXPOSE 80 

WORKDIR /var/www/

CMD ["/usr/bin/supervisord", "-n"]
