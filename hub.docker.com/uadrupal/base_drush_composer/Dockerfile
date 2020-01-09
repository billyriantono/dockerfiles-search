FROM php:7.3.9-cli-buster

ENV COMPOSER_ALLOW_SUPERUSER=1 \
  COMPOSER_HOME='/composer' \
  COMPOSER_VERSION='1.9.0' \
  DRUSH_VERSION='8.3.0' \
  PATH="/composer/vendor/bin:${PATH}"

RUN set -e \
  && apt-get update \
  && apt-get install -y \
    git \
    libbz2-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libldap2-dev \
    libxslt1.1 \
    libxslt1-dev \
    libzip-dev \
    ucf \
    wget \
    zip \
  && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
  && docker-php-ext-install -j$(nproc) \
    bcmath \
    bz2 \
    gd \
    ldap \
    pdo_mysql \
    xsl \
    zip \
  && ln -fs /usr/share/zoneinfo/America/Phoenix /etc/localtime \
  && dpkg-reconfigure -f noninteractive tzdata \
  && rm -r /var/lib/apt/lists/* \
  && mv "${PHP_INI_DIR}/php.ini-production" "${PHP_INI_DIR}/php.ini" \
  && echo 'memory_limit=-1' > "${PHP_INI_DIR}/conf.d/memory-limit.ini" \
  && echo "date.timezone=${PHP_TIMEZONE:-America/Phoenix}" > "${PHP_INI_DIR}/conf.d/date_timezone.ini" \
  && installer='/tmp/installer.php' \
  && curl -fsSL -o "$installer" 'https://getcomposer.org/installer' \
  && sig_expect=$(curl -fsSL 'https://composer.github.io/installer.sig' ) \
  && sig_got=$(php -r "echo hash_file('SHA384', '${installer}');") \
  && [ "$sig_got" = "$sig_expect" ] \
  && php "$installer" --no-ansi --install-dir='/usr/local/bin' --filename=composer --version="$COMPOSER_VERSION" \
  && rm "$installer" \
  && composer --ansi --version --no-interaction \
  && drushpath="/usr/local/bin/drush" \
  && curl -fsSL -o "$drushpath" "https://github.com/drush-ops/drush/releases/download/${DRUSH_VERSION}/drush.phar" \
  && chmod 755 "$drushpath" \
  && drush core-status
