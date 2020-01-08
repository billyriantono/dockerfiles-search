ARG PHP_VERSION=5.6
ARG PHP_VARIANT=apache
ARG PHP_TAG=${PHP_VERSION}-${PHP_VARIANT}
ARG PHP_IMAGE=php:${PHP_TAG}
ARG PHP_EXT_INSTALL="\
    bcmath \
    curl \
    gd \
    intl \
    mbstring \
    mysqli \
    pdo \
    pdo_mysql \
    simplexml \
    soap \
    xml \
    xsl \
    zip \
"
ARG PHP_EXT_REQUIRE="\
    ${PHP_EXT_INSTALL} \
"
ARG PHP_EXT_BUILD_DEPS="\
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libcurl4-openssl-dev \
    libpng-dev \
    libicu-dev \
    libmcrypt-dev \
    libxml2-dev \
    libxslt-dev \
    libzip-dev \
"

ARG RUN_DEPS="\
    libfreetype6 \
    libjpeg62-turbo \
    libmcrypt4 \
    libpng16-16 \
    libxslt1.1 \
    libzip4 \
    msmtp \
"

FROM ${PHP_IMAGE} as php-extensions
ARG PHP_EXT_INSTALL
ARG PHP_EXT_BUILD_DEPS

RUN echo ${PHP_EXT_INSTALL} > /php-ext-install
RUN if [ `printf '%s\n%s\n' "${PHP_VERSION}" "7.0" | sort -V | sed '1q'` != "7.0" ]; then echo mysql >> /php-ext-install; fi
RUN if [ `printf '%s\n%s\n' "${PHP_VERSION}" "7.2" | sort -V | sed '1q'` != "7.2" ]; then echo mcrypt >> /php-ext-install; fi
RUN apt-get update && apt-get install -y ${PHP_EXT_BUILD_DEPS} --no-install-recommends
RUN mkdir -p /usr/include/freetype2/freetype
RUN printf '#!/bin/sh\nexec pkg-config "$@" freetype2\n' > /usr/local/bin/freetype-config
RUN chmod +x /usr/local/bin/freetype-config
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install `cat /php-ext-install`

FROM ${PHP_IMAGE} as composer
ARG COMPOSER_SHA384=a5c698ffe4b8e849a443b120cd5ba38043260d5c4023dbf93e1558871f1f07f58274fc6f4c93bcfd858c6bd0775cd8d1
WORKDIR /tmp
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('sha384', 'composer-setup.php') === '${COMPOSER_SHA384}') exit(0); exit(1);"
RUN php composer-setup.php
RUN chmod a+x composer.phar

FROM ${PHP_IMAGE}
ARG PHP_EXT_REQUIRE
ARG RUN_DEPS

COPY --from=php-extensions /usr/local/lib/php /usr/local/lib/php
COPY --from=php-extensions /usr/local/include/php /usr/local/include/php
COPY --from=php-extensions /usr/local/etc/php /usr/local/etc/php
COPY --from=php-extensions /php-ext-install /php-ext-install
COPY --from=composer /tmp/composer.phar /usr/bin/composer.phar
RUN set -ex \
 && apt-get update && apt-get install -y ${RUN_DEPS} --no-install-recommends && rm -rf /var/lib/apt/lists/* \
 && php -r '\
    $extensions = $_SERVER["argv"]; array_shift($extensions);\
    foreach ($extensions as $extension) {\
      if (!extension_loaded($extension)) {\
        file_put_contents("php://stderr", "Required extension \"$extension\" not loaded\n");\
        exit(1); \
      }\
    }\
    exit(0);\
  ' `cat /php-ext-install` ${PHP_EXT_REQUIRE} \
 && rm -f /php-ext-install
