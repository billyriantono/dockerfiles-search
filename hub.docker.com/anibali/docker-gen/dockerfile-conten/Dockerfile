FROM php:7.2-apache
MAINTAINER angelomsq <angelomsq@gmail.com>

RUN apt-get update && apt-get install -y \
	locales

COPY config/app.conf /etc/apache2/sites-available/
RUN a2ensite app.conf
RUN a2dissite 000-default.conf
RUN a2enmod rewrite

RUN echo "en_US UTF-8" >> /etc/locale.gen
RUN echo "pt_BR UTF-8" >> /etc/locale.gen
RUN locale-gen

# install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install nodejs
#RUN curl -sL https://deb.nodesource.com/setup_8.x | bash - \
#	&& apt-get install -y nodejs \
#	&& npm update -g npm \
#	&& npm install -g gulp protractor jscs jshint typescript typings \
#	&& webdriver-manager update

RUN docker-php-ext-install pdo_mysql

WORKDIR /var/www

CMD ["apachectl", "-D", "FOREGROUND"]

Expose 80 443