FROM php:7.2.1-apache-stretch
ARG DEBIAN_FRONTEND=noninteractive

ENV LETSENCRYPT_HOME /etc/letsencrypt

RUN apt-get update && apt-get install -my wget gnupg \
    && echo 'deb http://ftp.debian.org/debian stretch-backports main' >> /etc/apt/sources.list \
    && curl -sS http://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
    && echo "deb http://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
    && apt-get update \
    && apt-get install -y supervisor \
    && mkdir -p /var/log/supervisor \
    && apt-get install -y dialog \
    && apt-get install -y git \
    && apt-get install -y zip \
    && apt-get install -y unzip \
    && apt-get install -y vim \
    && apt-get install -y apt-utils \
    && apt-get install -y libnotify-bin \
    && apt-get install -y sendmail \
    && apt-get install -y build-essential patch \
    && apt-get install -y rsyslog \
    && a2enmod rewrite \
    # https://github.com/docker-library/php/issues/105#issuecomment-196273150
    && apt-get install -y libmagickwand-dev --no-install-recommends \
    && a2enmod ssl \
    && a2enmod headers \
    && a2enmod actions \
    && apt-get install -y python-certbot-apache -t stretch-backports \
    && pecl install imagick \
    && docker-php-ext-enable imagick \
    && docker-php-ext-install pcntl \
    && docker-php-ext-install soap \
    && docker-php-ext-install bcmath \
    && apt-get install -y libpq-dev \
    && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
    && docker-php-ext-install mysqli pdo pdo_mysql pdo_pgsql \
    && apt-get install -y libmcrypt-dev \
    && pecl install mcrypt-1.0.1 \
    && docker-php-ext-enable mcrypt \
    && apt-get install -y libssl-dev \
    && pecl install mongodb \
    && apt-get install curl -y \
    && curl -sL https://deb.nodesource.com/setup_6.x | bash - \
    && apt-get install -y nodejs \
    && npm install -g bower \
    && apt-get install yarn \
    && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php -r "if (hash_file('SHA384', 'composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
    && php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
    # && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && chmod -R 755 /var/www/html \
    && chown -R www-data:www-data /var/www/html \
    && chmod -R 644 /etc/cron.d/* \
    && chown -R root:root /etc/cron.d/* \
    && echo "postfix postfix/main_mailer_type string 'Internet Site'" | debconf-set-selections \
    && echo "postfix postfix/mailname string $(hostname -f)" | debconf-set-selections \
    && apt-get install -y postfix \
    && postconf -e "inet_interfaces = loopback-only" \
    && postconf -e "debug_peer_level = 2"

COPY config/php.ini /usr/local/etc/php
RUN ln -sfT /dev/stderr "$APACHE_LOG_DIR/error.log"

COPY config/supervisord.conf /etc/supervisor/supervisord.conf
COPY config/scripts/pmg-* /usr/local/bin/
RUN chmod +x /usr/local/bin/pmg-*

ENV TZ=America/Chicago
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

CMD ["/usr/bin/supervisord"]
