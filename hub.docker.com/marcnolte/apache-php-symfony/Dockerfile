FROM php:7.3.1-apache
MAINTAINER Marc Nolte <contact@marcnolte.nl>

# install required packages
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        cmake \
        libbz2-dev \
        libfreetype6-dev \
        libgd-dev \
        libgmp-dev \
        libjpeg62-turbo-dev \
        libmagickwand-dev \
        libmagickwand-6.q16-3 \
        libmcrypt-dev \
        libpng-dev \
        libtidy-dev \
        libxml2-dev \
        libxslt-dev \
        libzip-dev \
        libzmq3-dev \
        mysql-client \
        zip \
        zlib1g-dev \
    && rm -rf /var/lib/apt/lists/*

# build ICU 63.1 from sources (for intl ext)
ENV PHP_CPPFLAGS="$PHP_CPPFLAGS -std=c++11"
RUN curl -LsS http://download.icu-project.org/files/icu4c/63.1/icu4c-63_1-src.tgz -o /tmp/icu.tgz \
    && tar -zxf /tmp/icu.tgz -C /tmp \
    && cd /tmp/icu/source \
    && ./configure --prefix=/usr/local \
    && make \
    && make install \
    && rm -rf /tmp/icu* \
    && docker-php-ext-configure intl --with-icu-dir=/usr/local \
    && docker-php-ext-install -j$(nproc) intl

# install tidy-html5
RUN curl -LsS https://codeload.github.com/htacg/tidy-html5/tar.gz/5.6.0 -o /tmp/tidy.tgz \
    && tar -zxf /tmp/tidy.tgz -C /tmp \
    && cd /tmp/tidy-html5-5.6.0/build/cmake \
    && cmake ../.. -DCMAKE_BUILD_TYPE=Release \
    && make install \
    && rm -rf /tmp/tidy* \
    && docker-php-ext-configure tidy --with-tidy=/usr/local \
    && docker-php-ext-install -j$(nproc) tidy

# install precision math
RUN ln -s /usr/include/x86_64-linux-gnu/gmp.h /usr/include/gmp.h \
    && docker-php-ext-install -j$(nproc) gmp bcmath

# install image processing
RUN pecl install imagick \
    && docker-php-ext-enable imagick \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

# install compression
RUN docker-php-ext-configure zip --with-libzip \
    && docker-php-ext-install -j$(nproc) zip

# install common extensions
RUN docker-php-ext-install -j$(nproc) \
    bz2 \
    gettext mbstring \
    mysqli pdo pdo_mysql \
    soap sockets \
    dom xmlrpc xsl \
    iconv \
    exif \
    opcache

# install mcrypt 1.0.2
RUN pecl install mcrypt-1.0.2 \
    && docker-php-ext-enable mcrypt

# install apcu
RUN pecl install apcu \
  && docker-php-ext-enable apcu

# install xdebug 2.7.0RC2
RUN pecl install xdebug-2.7.0RC2 \
    && docker-php-ext-enable xdebug

# install configuration
COPY config/apache2.conf /etc/apache2/apache2.conf
COPY config/app.conf /etc/apache2/sites-available/000-default.conf
COPY config/php.ini /usr/local/etc/php/php.ini

# enable apache modules
RUN a2enmod rewrite

# expose ports
EXPOSE 80 8080

WORKDIR /srv
CMD [ "apache2-foreground" ]
