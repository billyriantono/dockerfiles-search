FROM ubuntu:18.04

RUN apt-get update \
   && DEBIAN_FRONTEND=noninteractive apt-get install -y tzdata software-properties-common \
   && add-apt-repository -y ppa:ondrej/php \
   && apt-get update \
   && apt-get install -y --no-install-recommends \
	apache2 \
	php7.3 \
	libapache2-mod-php7.3 \
	php7.3-cli \
	php7.3-common \
	php7.3-curl\
	php7.3-dev\
	php7.3-mbstring \
	php7.3-gd \
	php7.3-intl \
	php7.3-xml \
	php7.3-mysql \
	php7.3-zip \
	git \
	gcc \
	curl \
	mysql-client \
	emacs25-nox \
	less \
	unzip \
#	php7.3-mcrypt \
#	libmcrypt-dev \
#	libreadline-dev \
#	php-pear \
    && rm -r /var/lib/apt/lists/*

RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf

WORKDIR /tmp

COPY composer-setup.php composer-setup.php
RUN  php composer-setup.php --install-dir=/usr/local/bin --filename=composer

RUN a2enmod rewrite \
    && a2enmod headers
COPY apache.conf /etc/apache2/sites-available/000-default.conf

RUN ln -sf /dev/stdout /var/log/apache2/access.log \
    && ln -sf /dev/stderr /var/log/apache2/error.log

# mcrypt for php7.3  ref. https://websiteforstudents.com/install-php-7-2-mcrypt-module-on-ubuntu-18-04-lts/
#RUN pecl channel-update pecl.php.net && pecl install mcrypt-1.0.1
#RUN echo "extension=mcrypt.so" >> /etc/php/7.3/cli/php.ini

COPY start-container /usr/local/bin/start-container
RUN chmod +x /usr/local/bin/start-container

## xdebug
RUN apt-get update && apt-get install -y --no-install-recommends \
            php7.3-dev \
    		php7.3-xdebug \
    	&& rm -rf /var/lib/apt/lists/*

COPY xdebug.ini /etc/php/7.3/mods-available/xdebug.ini

# make the terminal prettier 
COPY .bash_profile /root/.bash_profile

# Pass the DEVELOPER_EMAIL env var from the host (developer's) machine to the container
ENV DEVELOPER_EMAIL=$DEVELOPER_EMAIL
ENV VERSANTUS_ENV=dev

EXPOSE 80
CMD ["start-container"]