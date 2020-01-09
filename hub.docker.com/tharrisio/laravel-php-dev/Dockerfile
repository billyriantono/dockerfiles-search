FROM tharrisio/laravel-php

RUN apt-get -yqq update \
    && apt-get install -y --no-install-recommends \
        gnupg \
        git \ 
        ;

RUN curl --silent --location https://deb.nodesource.com/setup_8.x | bash -

RUN apt-get -yqq update \
    && apt-get install -y --no-install-recommends \
        nodejs \
        sqlite3 \
        libsqlite3-dev \
        libzip-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    ;

RUN npm install -g yarn

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php -r "if (hash_file('SHA384', 'composer-setup.php') === '93b54496392c062774670ac18b134c3b3a95e5a5e5c8f1a9f115f203b75bf9a129d5daa8ba6a13e2cc8a1da0806388a8') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && mv composer.phar /usr/local/bin/composer \
    ;

RUN pecl install xdebug-2.6.0 \
    && pecl install zip \
    && docker-php-ext-enable xdebug zip \
    && pecl install mongodb \
    && echo "extension=mongodb.so" > /usr/local/etc/php/conf.d/ext-mongodb.ini \
    ;

COPY xdebug.ini /usr/local/etc/php/conf.d/

WORKDIR /app
