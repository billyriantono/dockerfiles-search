FROM php:7.0-fpm

# Install mbstring
RUN docker-php-ext-install mbstring

# Install mcrypt
RUN apt-get update && apt-get install --no-install-recommends -y libmcrypt-dev && docker-php-ext-install mcrypt

# Install intl
RUN apt-get update && apt-get install --no-install-recommends -y libicu-dev \
  && docker-php-ext-configure intl \
  && docker-php-ext-install intl

# Install gd
RUN apt-get update && apt-get install --no-install-recommends -y libfreetype6-dev libjpeg62-turbo-dev libpng12-dev \
  && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
  && docker-php-ext-install gd

# Install zip
RUN docker-php-ext-install zip

# Install pdo_pgsql
RUN apt-get update && apt-get install --no-install-recommends -y libpq-dev \
  && docker-php-ext-install pdo_pgsql

# Install pdo_mysql
RUN docker-php-ext-install pdo_mysql

# Install opcache
RUN docker-php-ext-enable opcache

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install bash_completion
RUN apt-get update && apt-get install --no-install-recommends -y bash-completion \
  && curl -L https://raw.githubusercontent.com/yiisoft/yii2/master/contrib/completion/bash/yii -o /etc/bash_completion.d/yii

# Install xdebug
RUN pecl install xdebug

# Install imagick
RUN apt-get install --no-install-recommends -y libmagickwand-dev && pecl install imagick

# Clean repository
RUN apt-get clean && rm -rf /var/lib/apt/lists/*
