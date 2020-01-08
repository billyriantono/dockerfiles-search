FROM php:7.2.10-fpm-alpine
MAINTAINER Ivan Peevski <ivan@personifycare.com>

# Install dependencies
RUN  apk update && apk add --no-cache \
        freetype-dev \
        libjpeg-turbo-dev \
#        libmcrypt-dev \
        libpng-dev \
        icu-dev \
        gmp-dev \
        ghostscript \
        imagemagick-dev \
        imagemagick \
        git \
        curl \
        rsync \
        unzip \
        busybox-extras \
        openssh-client

# Install AWS
RUN apk add --no-cache jq python && \
    curl "https://s3.amazonaws.com/aws-cli/awscli-bundle.zip" -o "awscli-bundle.zip" && \
    unzip awscli-bundle.zip && \
    ./awscli-bundle/install -b /usr/local/bin/aws && \
    rm -rf awscli-bundle* && \
    apk del python

# Configure PHP
RUN apk add --no-cache gcc musl-dev linux-headers libffi-dev make autoconf && \
    ln -s /usr/include/x86_64-linux-gnu/gmp.h /usr/local/include/ \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-configure gmp \
    && docker-php-ext-install gd \
#    && docker-php-ext-install mcrypt \
    && docker-php-ext-install gmp \
    && docker-php-ext-install pcntl \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install sockets \
    && docker-php-ext-install intl \
    && docker-php-ext-install zip \
    && docker-php-ext-install opcache \
# Install PECL extensions
    && pecl install -o -f \
        imagick \
        redis \
        xdebug \
    && rm -rf /tmp/pear \
    && docker-php-ext-enable imagick \
    && docker-php-ext-enable redis \
    && docker-php-ext-enable xdebug \
# Clean up
    && apk del gcc musl-dev linux-headers libffi-dev make autoconf \
# Configure Xdebug extension
#    && echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_enable=1" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_autostart=1" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_connect_back=1 " >> /usr/local/etc/php/conf.d/xdebug.ini \
# Configure PHP
    && echo "max_input_vars=5000" > /usr/local/etc/php/conf.d/limits.ini \
    && echo "upload_max_filesize=8M" >> /usr/local/etc/php/conf.d/limits.ini \
    && echo "memory_limit=512M" >> /usr/local/etc/php/conf.d/limits.ini \
# Install composer
    && curl -fsSL https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && composer global require hirak/prestissimo

# Deal with potential security policy, blocking imagick from reading PDFs
RUN sed -i -e 's/rights="none" pattern="PDF"/rights="read" pattern="PDF"/' /etc/ImageMagick-7/policy.xml

RUN apk add --no-cache npm \
    && npm install --global purgecss stylelint stylelint-config-default eslint

ENV PATH="vendor/bin:${PATH}"

CMD ["sh"]

