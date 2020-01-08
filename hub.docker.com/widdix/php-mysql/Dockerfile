FROM php:5.6-apache

RUN apt-get update && apt-get install -y rsync && rm -r /var/lib/apt/lists/*

RUN a2enmod rewrite

# install the PHP extensions we need
RUN apt-get update && apt-get install -y libpng12-dev sendmail imagemagick && rm -rf /var/lib/apt/lists/* \
	&& docker-php-ext-install gd \
	&& apt-get purge --auto-remove -y libpng12-dev
RUN docker-php-ext-install mysqli

COPY php.ini /usr/local/etc/php/php.ini

COPY start.sh /start.sh
RUN chmod +x /start.sh

CMD /start.sh