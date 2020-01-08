FROM php:7.1-fpm

ADD bin/docker-* /usr/bin/

# Extensions
RUN apt-get update && apt-get install -y \
        git \
        libtool \
        automake \
        build-essential \
        librabbitmq-dev \
        libicu-dev \
        libjpeg-dev \
        libpng12-dev \
        libfreetype6-dev && \
    docker-php-ext-configure gd \
        --enable-gd-native-ttf \
        --with-jpeg-dir=/usr/lib/x86_64-linux-gnu \
        --with-png-dir=/usr/lib/x86_64-linux-gnu \
        --with-freetype-dir=/usr/lib/x86_64-linux-gnu && \
    docker-php-ext-install \
	    bcmath \
        zip \
        mbstring \
        intl \
        opcache \
        pdo_mysql \
        gd && \
    echo "date.timezone = Europe/Paris" >> $PHP_INI_DIR/conf.d/app.ini

# APCU ext
RUN pecl install apcu-5.1.8 \
    && docker-php-ext-enable apcu

# Composer
RUN curl -k -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Download the rabbitmq-c library
# Install librabbitmq (required for compiling libraries)
#RUN git clone git://github.com/alanxz/rabbitmq-c.git \
#    && cd rabbitmq-c \
#    && git submodule init \
#    && git submodule update \
#    && autoreconf -i && ./configure && make && make install \
#    && pecl install amqp \
#    && echo "extension = amqp.so" >> $PHP_INI_DIR/conf.d/app.ini

WORKDIR /srv
