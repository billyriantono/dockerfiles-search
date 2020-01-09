FROM ubuntu:16.04

LABEL Author="Leonardo Cavalcante do Prado leonardo.prado@sysvale.com" 

# Install base dependencies
RUN apt-get update \
	&& apt-get upgrade -y \
	&&  apt-get install -y software-properties-common \
	curl \
	git \
	language-pack-en-base

# Add PHP ondrej repository
RUN LC_ALL=en_US.UTF-8 add-apt-repository ppa:ondrej/php && apt-get update

# Install php and its libraries
RUN apt -y install php7.2 \
	php7.2-mbstring \
	php7.2-xml \
	php7.2-curl \
	php7.2-mysql \
	php7.2-pgsql \
	php7.2-imagick \
	php7.2-zip \
	libxrender1 \
	libfontconfig1 \
	libxtst6 \
	php-mongodb \
	php-mongo

# Install nodejs and npm
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash - \
    && apt-get install -y nodejs \
    && npm install -g n npm@latest \
    && n 8.10

# Install composer
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer
ENV PATH ${PATH}:/sbin:/bin:/usr/sbin:/usr/bin:/usr/local/sbin:/usr/local/bin:./vendor/bin:/composer/vendor/bin
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
	&& php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
	&& php -r "unlink('composer-setup.php');"

# Install php code sniffer
RUN composer global require "squizlabs/php_codesniffer=*"

RUN update-alternatives --set php /usr/bin/php7.2

WORKDIR /home/project-folder
