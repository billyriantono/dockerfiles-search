FROM graffine/commitizen:latest

# Add required php7 extensions
RUN apk upgrade -U && \
    apk --no-cache --update --repository=http://dl-4.alpinelinux.org/alpine/edge/testing add \
    bash \
    curl \
    git \
    openssh-client \
    php7-curl \
    php7-ctype \
    php7-dom \
    php7-fileinfo \
    php7-gd \
    php7-iconv \
    php7-json \
    php7-mbstring \
    php7-openssl \
    php7-pdo \
    php7-pdo_mysql \
    php7-session \
    php7-pdo_sqlite \
    php7-phar \
    php7-simplexml \
    php7-tokenizer \
    php7-xdebug \
    php7-xml \
    php7-xmlwriter \
    php7-zlib

# Add the composer.json
COPY ./composer.json /root/.composer/composer.json
COPY ./xdebug.ini /etc/php7/conf.d/xdebug.ini

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN composer global install \
  # Install php_codesniffer
  && composer global require friendsofphp/php-cs-fixer squizlabs/php_codesniffer \
  && ln -s ~/.composer/vendor/friendsofphp/php-cs-fixer/php-cs-fixer /usr/local/bin/php-cs-fixer \
  && ln -s ~/.composer/vendor/squizlabs/php_codesniffer/bin/phpcs /usr/local/bin/phpcs \
  && ln -s ~/.composer/vendor/squizlabs/php_codesniffer/bin/phpcbf /usr/local/bin/phpcbf

#
#--------------------------------------------------------------------------
# Final Touch
#--------------------------------------------------------------------------
#

RUN apk del curl && \
    rm -fr /var/cache/apk/*

