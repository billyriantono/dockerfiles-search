FROM php:7.0.14-cli
MAINTAINER halito! <devs@halito.com>

#
# Update
#
RUN apt-get update -y

#
# Install Zip and GIT
#
RUN apt-get install -y \
    zip \
    unzip \
    git

#
# Download AWS CLI dependencies
#
RUN apt-get install python-pip -y
RUN apt-get install python-software-properties -y

#
# Install AWS CLI
#
RUN pip install awscli

#
# Install Composer
#
RUN curl -s http://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

#
# Install PHPUnit
#
RUN cd /tmp \
    && curl -O https://phar.phpunit.de/phpunit.phar \
    && chmod +x phpunit.phar \
    && mv phpunit.phar /usr/local/bin/phpunit

#
# Enable Apache modules
#
#RUN a2enmod rewrite
#RUN a2enmod ssl

#
# Download extension dependencies
#
RUN apt-get install -y \
    libcurl3-dev \
    libxml2-dev \
    libzzip-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libicu-dev \
    libedit-dev \
    && rm -rf /var/lib/apt/lists/*

#
# Install extensions
#
RUN docker-php-ext-install pdo \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install curl \
    && docker-php-ext-install xml \
    && docker-php-ext-install calendar \
    && docker-php-ext-install zip \
    && docker-php-ext-install gd \
    && docker-php-ext-install bcmath \
    && docker-php-ext-install mbstring \
    && docker-php-ext-install mcrypt \
    && docker-php-ext-install intl \
    && docker-php-ext-install readline

#
# Configure extension
#
RUN docker-php-ext-configure gd \
    --with-freetype-dir=/usr/include/ \
    --with-jpeg-dir=/usr/include/

RUN docker-php-ext-configure calendar \
    --enable-calendar

RUN docker-php-ext-configure readline \
    --with-readline

#
# Enable extension
#
RUN docker-php-ext-enable readline

#
# Install NodeJS and it's dependencies
#
RUN curl -sL https://deb.nodesource.com/setup_7.x | bash -
RUN apt-get install -y nodejs

COPY gulpfile.js ./gulpfile.js
COPY package.json ./package.json

RUN npm install gulp-cli -g && npm install gulp
RUN npm install del


