FROM johnpbloch/phpfpm:7.1

RUN curl -L https://phar.phpunit.de/phpunit.phar > /tmp/phpunit.phar \
	&& chmod +x /tmp/phpunit.phar \
	&& mv /tmp/phpunit.phar /usr/local/bin/phpunit

RUN apt-get update && apt-get install -y \
	git \
	subversion \
	wget \
	libxml2-dev \
	ssmtp \
	imagemagick \
	libmagickwand-dev \
	libpq-dev \
	libzip-dev \
	libicu-dev \
	libpng12-dev \
	libjpeg62-turbo-dev \
	libfreetype6-dev \
	unzip

RUN pecl install imagick
RUN docker-php-ext-enable imagick

RUN docker-php-ext-install soap

RUN apt-get  && apt-get install -y \
	postgresql \
	postgresql-contrib \
  	sudo

RUN docker-php-ext-install \
        pdo \
        pdo_pgsql \
        pgsql \
        sockets \
        intl

# RUN apt-get update \
#   && apt-get install -y postgresql postgresql-contrib \
#   && apt-get install sudo \
#   && docker-php-ext-install pdo pdo_pgsql

# RUN echo "deb http://ftp.de.debian.org/debian stretch main" >> /etc/apt/sources.list
# RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y postgresql postgresql-contrib phppgadmin
# RUN apt-get install -y php-pgsql

RUN echo "mailhub=mailcatcher:1025\nUseTLS=NO\nFromLineOverride=YES" > /etc/ssmtp/ssmtp.conf

RUN apt-get remove -y libmagickwand-dev libxml2-dev && \
	apt-get autoremove -y && \
	apt-get clean

CMD ["php-fpm"]

EXPOSE 9000