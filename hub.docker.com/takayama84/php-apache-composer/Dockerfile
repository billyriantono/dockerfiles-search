FROM php:7.1.6-apache

# RUN docker-php-source extract \
#     && docker-php-ext-configure zip --with-zlib-dir=/var/lib/dpkg/info \
#     && docker-php-ext-install -j$(nproc) zip \
# && docker-php-source delete

# RUN docker-php-ext-configure zip --with-libzip-dir=/usr/bin \
# && docker-php-ext-install -j$(nproc) zip

# RUN docker-php-ext-enable zip

# RUN docker-php-source extract \
#     && docker-php-ext-install -j$(nproc) libzip \
# && docker-php-source delete

# RUN docker-php-source extract \
#     && docker-php-ext-enable zip \
# && docker-php-source delete

# RUN curl -fsSL 'http://hg.nih.at/libzip/archive/tip.tar.gz' -o libzip.tar.gz \
#     && mkdir -p /tmp/libzip \
#     && tar -xf libzip.tar.gz -C /tmp/libzip --strip-components=1 \
#     && rm libzip.tar.gz \
#     && docker-php-ext-configure /tmp/libzip --enable-libzip \
#     && docker-php-ext-install /tmp/libzip \
#     && rm -r /tmp/libzip

# installing zlib
RUN mkdir -p /usr/src/zlib
WORKDIR /usr/src/zlib
RUN curl -fsSL 'https://zlib.net/zlib-1.2.11.tar.gz' -o zlib.tar.gz \
    && tar zxvf zlib.tar.gz \
    && cd zlib-1.2.11 \
    && ./configure && make && make install

# installing libzip
RUN mkdir -p /usr/src/libzip
WORKDIR /usr/src/libzip
RUN curl -fsSL 'https://nih.at/libzip/libzip-1.2.0.tar.gz' -o libzip.tar.gz \
    && tar zxvf libzip.tar.gz \
    && cd libzip-1.2.0 \
    && ./configure && make && make install

# installing composer
RUN mkdir -p /usr/local/bin/composer
WORKDIR /usr/local/bin/composer
RUN /usr/local/bin/php -r "readfile('https://getcomposer.org/installer');" | /usr/local/bin/php
ENV PATH $PATH:/usr/local/bin:/usr/local/bin/composer

# set workdir
WORKDIR /var/www/html

# set volume
VOLUME /var/www/html
