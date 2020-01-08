FROM php:5.5.25-fpm

# --- SOFT --- #

RUN apt-get update && apt-get install -y \
    tzdata \
    openssh-client \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng12-dev \
    zlib1g-dev \
    libssl-dev \
    libreadline-dev \
    g++ \
    libmemcached-dev \
    imagemagick \
    libmagickwand-6.q16-dev --no-install-recommends \
    wget \
    bzip2 \ 
    sendmail \
    git

RUN ln -s /usr/lib/x86_64-linux-gnu/ImageMagick-6.8.9/bin-Q16/MagickWand-config /usr/bin

# --- RUBY --- #

ENV PATH="/root/.rbenv/bin:/root/.rbenv/shims:${PATH}"
RUN curl -fsSL https://github.com/rbenv/rbenv-installer/raw/master/bin/rbenv-installer | bash && rbenv install 2.3.0 && rbenv global 2.3.0 && echo 'eval "$(rbenv init -)"' >> ~/.bashrc

# --- ICU --- #

RUN mkdir /opt/tmp && cd /opt/tmp && \
    wget http://download.icu-project.org/files/icu4c/58.2/icu4c-58_2-src.tgz && \
    tar zxvf icu4c-58_2-src.tgz && \
    cd icu/source && \
    ./configure --prefix=/opt/icu582 && make && make install && \
    rm -rf /opt/tmp

# --- EXTENSIONS --- #

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-install gd && \
    docker-php-ext-install opcache && \
    docker-php-ext-install zip && \
    docker-php-ext-install mysql && \
    docker-php-ext-install pdo_mysql && \
    docker-php-ext-install mysqli && \
    docker-php-ext-install mbstring && \
    docker-php-ext-configure intl --with-icu-dir=/opt/icu582 && \
    docker-php-ext-install intl

RUN pecl channel-update pecl.php.net && \
    pecl install redis-2.2.8 && \
    pecl install mongo && \
    pecl install memcache && \
    pecl install memcached-2.2.0 && \
    pecl install imagick

RUN echo "extension=mongo.so" > /usr/local/etc/php/conf.d/ext-mongo.ini && \
    echo "extension=redis.so" > /usr/local/etc/php/conf.d/ext-redis.ini && \
    echo "extension=memcache.so" > /usr/local/etc/php/conf.d/ext-memcache.ini && \
    echo "extension=memcached.so" > /usr/local/etc/php/conf.d/ext-memcached.ini && \
    echo "extension=imagick.so" > /usr/local/etc/php/conf.d/ext-imagick.ini

# --- NODE --- #

RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install -y nodejs

# --- COMPOSER --- #

RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

EXPOSE 9000

CMD ["php-fpm", "--allow-to-run-as-root"]
