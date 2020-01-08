FROM php:7.1-fpm-alpine3.8
MAINTAINER James Gilliland <jgilliland@apqc.org>

RUN apk -U upgrade \
  && apk add --virtual .apqc-build-deps \
    $PHPIZE_DEPS \
    pcre-dev libjpeg-turbo-dev libpng-dev gmp-dev yaml-dev libzip-dev \
    wget \
    sudo \
  && apk add \
    pcre libltdl libjpeg-turbo libpng gmp yaml libzip \
    mysql-client \
    msmtp \
  && touch /var/log/php-build.log \
    && docker-php-ext-configure gd --with-jpeg-dir=/usr/include/ >> /var/log/php-build.log \
    && docker-php-ext-configure zip --with-libzip=/usr/include/ >> /var/log/php-build.log \
    && docker-php-ext-install mysqli pdo_mysql gd gmp zip bcmath >> /var/log/php-build.log \
    && docker-php-ext-enable opcache \
  && echo "Building APCU" \
    && pecl install apcu >> /var/log/php-build.log \
    && docker-php-ext-enable apcu \
  && echo "Building PECL YAML" \
    && pecl install yaml-2.0.4 >> /var/log/php-build.log \
    && docker-php-ext-enable yaml \
  && echo "Building PECL Redis" \
    && pecl install redis >> /var/log/php-build.log \
    && docker-php-ext-enable redis \
  && echo "Installing NewRelic" \
    && mkdir -p /opt/newrelic \
    && rm -rf /etc/dpkg \
    && cd /opt/newrelic \
    && wget -r -nd --no-parent -Alinux-musl.tar.gz https://download.newrelic.com/php_agent/release/ >/dev/null 2>&1 \
    && tar zxf *linux-musl.tar.gz \
    && cd newrelic* \
    && NR_INSTALL_SILENT=true /bin/sh newrelic-install install \
    && rm /opt/newrelic/*.tar.gz \
    && find /opt/newrelic/newrelic*/agent/ -type f | grep -v $(readlink $(find /usr/local/lib -name newrelic.so)) | xargs rm \
  && echo "Building xdebug" \
    && pecl install xdebug-2.7.2 >> /var/log/php-build.log \
  && echo "Installing blackfire" \
    && version=$(php -r "echo PHP_MAJOR_VERSION.PHP_MINOR_VERSION;") \
    && curl -A "Docker" -o /tmp/blackfire-probe.tar.gz -D - -L -s https://blackfire.io/api/v1/releases/probe/php/alpine/amd64/${version} \
    && mkdir -p /tmp/blackfire \
    && tar zxpf /tmp/blackfire-probe.tar.gz -C /tmp/blackfire \
    && mv /tmp/blackfire/blackfire-*.so $(php-config --extension-dir)/blackfire.so \
    && printf "extension=blackfire.so\n" > ${PHP_INI_DIR}/conf.d/blackfire.ini \
    && rm -rf /tmp/blackfire /tmp/blackfire-probe.tar.gz \
    && wget https://packages.blackfire.io/binaries/blackfire-php/1.22.0/blackfire-php-alpine_amd64-php-72-zts.so \
    && mv blackfire-php-alpine_amd64-php-72-zts.so $(php-config --extension-dir)/blackfire2.so \
  && cd /var/log/ \
    && gzip php-build.log \
    && cp /tmp/nrinstall* ./ \
    && gzip nrinstall* \
  && apk del .apqc-build-deps \
  && rm -rf /tmp/* \
  && rm -rf /var/cache/apk/*

RUN mkdir -p /root/.ssh \
  && sed -i "3 a if [ \"\${NR_LICENSE_KEY}x\" != \"x\" ]; then sed -i -e 's/REPLACE_WITH_REAL_KEY/\${NR_LICENSE_KEY}/g' /usr/local/etc/php/conf.d/newrelic.ini; else sed -i -e 's/;newrelic.enabled = true/newrelic.enabled = false/g' /usr/local/etc/php/conf.d/newrelic.ini; fi" /usr/local/bin/docker-php-entrypoint

# This seems broken atm. Its better to run without health checks than with a broken one.
#RUN apk add --no-cache fcgi
#HEALTHCHECK --interval=10s --timeout=3s \
#  CMD SCRIPT_NAME=/ping SCRIPT_FILENAME=/ping REQUEST_METHOD=GET cgi-fcgi -bind -connect 127.0.0.1:9000 || exit 1

