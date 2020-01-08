FROM php:7.2.0-apache
# This image does not contains the folowing librairies as before: xfonts-75dpi xfonts-base gd
# It's generated as a more efficient way as the previous images and size is twice lower
# You should use "--squash" when building image, size will pass from 700mb to 400mb with the squash option.
LABEL maintainer="Generalmedia SA <webmaster@generalmedia.ch>"

ENV IMAGICK_VERSION 3.4.3
ENV PHP_REDIS_VERSION 3.1.4

# Install php libs
# - libicu-dev > Intl
# - libxslt1-dev > xsl/xml
# - zlib1g-dev > zip
# - libmagickwand-dev > imagick
RUN apt-get update \
    && apt-get install -y \
    libicu-dev \
    libmcrypt-dev \
    libxslt1-dev \
    zlib1g-dev \
    nano \
    cron \
    libmagickwand-dev \
    --no-install-recommends \
    && echo "Enable build-in php extensions" \
    && docker-php-ext-install -j$(nproc) opcache intl xsl zip bcmath mbstring \
    && echo "Install Imagick" \
    && cd /tmp \
    && curl https://pecl.php.net/get/imagick-$IMAGICK_VERSION.tgz -o imagick-$IMAGICK_VERSION.tgz \
    && tar xvzf imagick-$IMAGICK_VERSION.tgz \
    && cd imagick-$IMAGICK_VERSION \
    && phpize \
    && ./configure \
    && make install \
    && docker-php-ext-enable imagick \
    && rm -rf /tmp/imagick-$IMAGICK_VERSION* \
    && cd \
    && echo "Install redis" \
    && docker-php-source extract \
    && curl -L -o /tmp/redis.tar.gz https://github.com/phpredis/phpredis/archive/$PHP_REDIS_VERSION.tar.gz \
    && tar xfz /tmp/redis.tar.gz \
    && rm -r /tmp/redis.tar.gz \
    && mv phpredis-$PHP_REDIS_VERSION /usr/src/php/ext/redis \
    && docker-php-ext-install redis \
    && docker-php-source delete \
    && echo "Cleanup apt" \
    && apt-get autoremove --purge -y \
    && rm -rf /var/lib/apt/lists/*

# Install node-js from https://github.com/nodejs/docker-node/blob/master/9/Dockerfile
ENV NODE_VERSION 9.3.0
RUN ARCH= && dpkgArch="$(dpkg --print-architecture)" \
  && case "${dpkgArch##*-}" in \
    amd64) ARCH='x64';; \
    ppc64el) ARCH='ppc64le';; \
    s390x) ARCH='s390x';; \
    arm64) ARCH='arm64';; \
    armhf) ARCH='armv7l';; \
    i386) ARCH='x86';; \
    *) echo "unsupported architecture"; exit 1 ;; \
  esac \
  && curl -SLO "https://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-$ARCH.tar.xz" \
  && tar -xJf "node-v$NODE_VERSION-linux-$ARCH.tar.xz" -C /usr/local --strip-components=1 --no-same-owner \
  && rm "node-v$NODE_VERSION-linux-$ARCH.tar.xz" \
  && ln -s /usr/local/bin/node /usr/local/bin/nodejs

# install composer globally
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /home/.composer/
ENV COMPOSER_VERSION 1.5.6
RUN curl -s -f -L -o /tmp/installer.php https://raw.githubusercontent.com/composer/getcomposer.org/863c57de1807c99d984f7b56f0ea56ebd7e5045b/web/installer \
 && php -r " \
    \$signature = '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061'; \
    \$hash = hash('SHA384', file_get_contents('/tmp/installer.php')); \
    if (!hash_equals(\$signature, \$hash)) { \
        unlink('/tmp/installer.php'); \
        echo 'Integrity check failed, installer is either corrupt or worse.' . PHP_EOL; \
        exit(1); \
    }" \
 && php /tmp/installer.php --no-ansi --install-dir=/usr/bin --filename=composer --version=${COMPOSER_VERSION} \
 && composer --ansi --version --no-interaction \
 && rm -rf /tmp/*

# Apache configuration
RUN a2enmod rewrite headers ssl deflate expires
COPY apache/000-default.conf /etc/apache2/sites-available/000-default.conf
COPY apache/000-dev.conf /etc/apache2/sites-available/000-dev.conf

COPY apache/deflate_gzip.conf /etc/apache2/mods-available/deflate_gzip.conf
RUN ln -sr /etc/apache2/mods-available/deflate_gzip.conf /etc/apache2/mods-enabled/
RUN a2ensite 000-dev 000-default

# Apache dev configuration
RUN openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /tmp/self-signed.key -out /tmp/self-signed.crt -subj /C=CH/ST=VD/L=Lausanne/CN=localhost
COPY apache/000-dev.conf /etc/apache2/sites-available/000-dev.conf
RUN rm -f /etc/apache2/sites-enabled/000-default.conf && ln -sr /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-enabled/000-default.conf


# PHP.ini
COPY php/*.ini /etc/php/7.2/mods-available/
RUN mkdir -p /etc/php/7.2/mods-enabled/ \
 && ln -sr /etc/php/7.2/mods-available/99-gm.ini /etc/php/7.2/mods-enabled/

# Create TMP dir.
# Note that you sould mount this as a volume to avoid docker-filesystem-expansion-bug
RUN mkdir -p /tmp/uploads/ && chmod +w -R /tmp/

COPY entrypoint.sh /var/www/entrypoint.sh
RUN chmod +x /var/www/entrypoint.sh
ENTRYPOINT ["/var/www/entrypoint.sh"]
