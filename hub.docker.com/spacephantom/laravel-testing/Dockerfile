FROM ubuntu:xenial

ENV DEBIAN_FRONTEND=noninteractive

# Install basics
RUN apt-get update
RUN apt-get install -y curl git ftp ncftp

# Install MySQL
RUN apt-get install -y mysql-server

# Install PHP 7.0
RUN apt-get install -y php7.0 php7.0-mysql php7.0-mcrypt php7.0-mbstring php7.0-cli php7.0-gd php7.0-curl php7.0-xml zip unzip php7.0-zip

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Allow Composer to be run as root
ENV COMPOSER_ALLOW_SUPERUSER 1

# Install phpunit
RUN curl --silent --show-error --location --output /usr/local/bin/phpunit https://phar.phpunit.de/phpunit-5.7.9.phar && \
  chmod +x /usr/local/bin/phpunit

# install nodejs and npm
RUN apt-get install -y nodejs
RUN ln -s /usr/bin/nodejs /usr/bin/node
RUN apt-get install -y npm

# install npm packages
RUN npm install -g gulp
