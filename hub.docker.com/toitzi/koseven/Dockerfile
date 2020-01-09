FROM ubuntu:16.04
MAINTAINER Tobias Oitzinger <tobiasoitzinger@gmail.com>

# Update packages and install apache + php7.0 + pecl
RUN DEBIAN_FRONTEND=noninteractive apt-get -y update && \
	apt-get -yq install --no-install-recommends \
	curl \
	gcc \
	php7.0 \
	php7.0-dev \
	php7.0-common \
	php7.0-cli \
	php7.0-mbstring \
	php7.0-gd \
	php7.0-mysql \
	php7.0-curl \
	php7.0-xml \
	php7.0-sqlite3 \
	php7.0-opcache \
	php7.0-pgsql \
	php7.0-mysql \
	php7.0-mcrypt \
	php-pear \
	php-raphf \
	php-raphf-dev \
	php-propro \
	php-propro-dev \
	php-http \
	php-pecl-http \
	php-redis \
	libcurl4-openssl-dev \
	libmagic-dev \
	apache2 \
	libapache2-mod-php7.0 \
	apache2

# Configuring apache2
RUN echo '<VirtualHost *:80>\n\tDocumentRoot /var/www/koseven/public/\n\n\t<Directory /var/www/koseven/public/>\n\t\tOptions Indexes FollowSymLinks\n\t\tAllowOverride All\n\t\tRequire all granted\n\t</Directory>\n</VirtualHost>\n' >> /etc/apache2/sites-enabled/koseven.conf && \
	a2enmod rewrite && \
	rm /etc/apache2/sites-enabled/000-default.conf && \
	mkdir -p /var/www/koseven/public/

EXPOSE 80

CMD service apache2 restart && \
	tail -F /var/log/apache2/*
