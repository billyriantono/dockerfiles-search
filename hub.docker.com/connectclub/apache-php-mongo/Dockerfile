FROM php:7.3-apache

COPY errors.ini /usr/local/etc/php/conf.d/errors.ini
COPY apache2.conf /etc/apache2/apache2.conf

RUN apt-get update && apt-get install libssl-dev -y && \
    apt-get install -y xfonts-75dpi fontconfig libx11-dev libjpeg62-turbo libxext6 libxrender1 xfonts-base \ 
    gnupg1 apt-transport-https && \
    curl -s https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add -                           && \
    echo 'deb https://deb.nodesource.com/node_11.x stretch main' > /etc/apt/sources.list.d/nodesource.list && \
    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -                                      && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" > /etc/apt/sources.list.d/yarn.list              && \
    mkdir /var/www/.npm && chown www-data:www-data /var/www/.npm                                           && \
    apt-get update && apt-get install -y nodejs yarn && rm -rf /var/lib/apt/lists/*

RUN a2enmod rewrite
RUN pecl install mongodb \
    && docker-php-ext-enable mongodb

RUN apt-get update && apt-get install -y libapache2-mod-geoip geoip-database-extra
COPY geoip.conf /etc/apache2/mods-available/geoip.conf
COPY remoteip.conf  /etc/apache2/mods-available/remoteip.conf
RUN a2enmod remoteip

RUN \
  curl -L https://download.newrelic.com/php_agent/release/newrelic-php5-9.3.0.248-linux.tar.gz | tar -C /tmp -zx && \
   export NR_INSTALL_USE_CP_NOT_LN=1 && \
    export NR_INSTALL_SILENT=1 && \
     /tmp/newrelic-php5-*/newrelic-install install && \
      rm -rf /tmp/newrelic-php5-* /tmp/nrinstall*

RUN curl http://de.archive.ubuntu.com/ubuntu/pool/universe/f/fonts-open-sans/fonts-open-sans_1.11-1_all.deb -o opensans.deb            && \
    curl -L https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.5/wkhtmltox_0.12.5-1.stretch_amd64.deb -o wkhtmltox.deb  && \
   dpkg -i opensans.deb wkhtmltox.deb                                                                                && \
   rm -rf wkhtmltox.deb opensans.deb

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
RUN mkdir /home/www-data && chown -R www-data:www-data /home/www-data
ENV COMPOSER_HOME /home/www-data/.composer
