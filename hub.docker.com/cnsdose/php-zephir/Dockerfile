ARG PHP_VERSION=7
ARG ZEPHIR_PARSER_VERSION=
ARG ZEPHIR_VERSION=

FROM php:${PHP_VERSION}

# apt wrapper
ADD apt-install /usr/bin/apt-install

# build tools
RUN apt-install gcc make re2c autoconf automake wget git

# php core extensions
RUN apt-install libgmp-dev libzip-dev
RUN ln -s /usr/local/etc/php/php.ini-development /usr/local/etc/php/php.ini
RUN docker-php-source extract
RUN docker-php-ext-install gmp
RUN docker-php-ext-install zip

# composer
WORKDIR /usr/bin
RUN wget https://raw.githubusercontent.com/composer/getcomposer.org/76a7060ccb93902cd7576b67264ad91c8a2700e2/web/installer -O - -q | php -- --quiet
RUN ln -s /usr/bin/composer.phar /usr/bin/composer

# zephir parser
WORKDIR /opt
RUN git clone https://github.com/phalcon/php-zephir-parser.git
WORKDIR /opt/php-zephir-parser
RUN if [ -z "$ZEPHIR_PARSER_VERSION" ]; then git checkout "$(git tag --sort=creatordate | tail -n 1)"; else git checkout "$ZEPHIR_PARSER_VERSION"; fi
RUN phpize
RUN ./configure
RUN make
RUN make install
RUN docker-php-ext-enable zephir_parser

# zephir
WORKDIR /opt
RUN git clone https://github.com/phalcon/zephir
WORKDIR /opt/zephir
RUN if [ -z "$ZEPHIR_VERSION" ]; then git checkout "$(git tag --sort=creatordate | tail -n 1)"; else git checkout "$ZEPHIR_VERSION"; fi
RUN composer install
RUN ln -s /opt/zephir/zephir /usr/bin/zephir

WORKDIR /opt
CMD bash
