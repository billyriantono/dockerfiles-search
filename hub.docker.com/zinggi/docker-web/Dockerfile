FROM php:5.6-apache

LABEL maintainer="Christian Zingg <mich-web@zinggi.ch>"

RUN apt-get clean && apt-get -y update && apt-get install -y locales && locale-gen en_US.UTF-8

# Set environment variables
ENV COMPOSER_ALLOW_SUPERUSER=1

# Install Libraries
RUN apt-get install --no-install-recommends -y \
        build-essential \
        curl \
        git \
        libcurl4-openssl-dev \
        libicu-dev \
        libmcrypt-dev \
        libpng-dev \
        graphicsmagick \
        imagemagick \
        libxml2-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        zlib1g-dev \
        default-mysql-client \
        software-properties-common \
        rsync \
        vim \
        zip \
        unzip

# Install PHP
RUN docker-php-ext-configure pdo_mysql --with-pdo-mysql=mysqlnd \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install \
      curl \
      gd \
      intl \
      json \
      mbstring \
      mysql \
      mysqli \
      pdo \
      pdo_mysql \
      zip \
      opcache

# Install Composer
RUN php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer

# Install mhsendmail
RUN curl -Lsf 'https://dl.google.com/go/go1.13.1.linux-amd64.tar.gz' | tar -C '/usr/local' -xvzf -
ENV PATH /usr/local/go/bin:$PATH
RUN go get github.com/mailhog/mhsendmail
RUN cp /root/go/bin/mhsendmail /usr/bin/mhsendmail
RUN echo 'sendmail_path = /usr/bin/mhsendmail --smtp-addr mailhog:1025' > /usr/local/etc/php/conf.d/sendmail.ini

# Apache configuration
RUN a2enmod rewrite
RUN a2enmod ssl

# Change uid and gid of apache to docker user uid/gid
RUN usermod -u 1000 www-data && groupmod -g 1000 www-data

# Add tools
ENV TOOLS_DIR /var/www/tools
RUN mkdir ${TOOLS_DIR}
ADD ./tools ${TOOLS_DIR}

# optimization: needed folders (without sync to host)
RUN mkdir -p /var/www/html/bin
RUN mkdir -p /var/www/html/var
RUN mkdir -p /var/www/html/public/typo3temp

# Change ownership
RUN chown -R www-data:www-data /var/www