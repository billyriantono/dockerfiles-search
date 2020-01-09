From php:5.6-apache
MAINTAINER Salif Guigma <salif.guigma@gmail.com>

RUN buildDeps=" \
            		libfreetype6-dev \
            		libjpeg-dev \
            		libmcrypt-dev \
            		libpng-dev \
            		zlib1g-dev \
          "; \
          set -x \
          && apt-get update && apt-get install -y  $buildDeps --no-install-recommends \
          libicu-dev \
          vim \
          git \
          openssh-client \
          cron \
          && apt-get clean \
          && rm -rf /var/lib/apt/lists/* \
          && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && \
    	      php /usr/local/bin/composer self-update \
          && curl -LsS https://symfony.com/installer -o /usr/local/bin/symfony && \
          	chmod a+x /usr/local/bin/symfony \
          && curl http://get.sensiolabs.org/php-cs-fixer.phar -o /usr/local/bin/php-cs-fixer && \
            chmod a+x /usr/local/bin/php-cs-fixer \
          && curl -sS -o /tmp/icu.tar.gz -L http://download.icu-project.org/files/icu4c/57.1/icu4c-57_1-src.tgz \
          && tar -zxf /tmp/icu.tar.gz -C /tmp \
          && cd /tmp/icu/source \
          && ./configure --prefix=/usr/local \
          && make && make install \
          && docker-php-ext-configure gd --enable-gd-native-ttf --with-jpeg-dir=/usr/lib/x86_64-linux-gnu --with-png-dir=/usr/lib/x86_64-linux-gnu --with-freetype-dir=/usr/lib/x86_64-linux-gnu \
          && docker-php-ext-install gd \
          && docker-php-ext-configure intl --with-icu-dir=/usr/local \
          && docker-php-ext-install zip pdo pdo_mysql opcache intl sockets mbstring bcmath \
          && a2enmod rewrite \
          && pecl install xdebug-2.5.5 \
          && pecl clear-cache \
          && echo "zend_extension=/usr/local/lib/php/extensions/no-debug-non-zts-20131226/xdebug.so" > /usr/local/etc/php/conf.d/xdebug.ini \
          && echo "xdebug.remote_enable=On" >> /usr/local/etc/php/conf.d/xdebug.ini \
          && echo "xdebug.remote_autostart=1" >> /usr/local/etc/php/conf.d/xdebug.ini \
          && echo "xdebug.remote_port=9000" >> /usr/local/etc/php/conf.d/xdebug.ini \
          && version=$(php -r "echo PHP_MAJOR_VERSION.PHP_MINOR_VERSION;") \
          && curl -A "Docker" -o /tmp/blackfire-probe.tar.gz -D - -L -s https://blackfire.io/api/v1/releases/probe/php/linux/amd64/$version \
          && tar zxpf /tmp/blackfire-probe.tar.gz -C /tmp \
          && mv /tmp/blackfire-*.so $(php -r "echo ini_get('extension_dir');")/blackfire.so \
          && printf "extension=blackfire.so\nblackfire.agent_socket=tcp://blackfire:8707\n" > $PHP_INI_DIR/conf.d/blackfire.ini \
          && pecl install apcu-4.0.11 \
          && docker-php-ext-enable apcu \
          && git clone https://github.com/fabpot/Twig.git /tmp/Twig \
          && cd /tmp/Twig/ext/twig && phpize && ./configure && make && make install \
          && usermod -u 1000 www-data \
          && groupmod -g 1000 www-data \
          && usermod -s /bin/bash www-data \
          && echo "date.timezone = Europe/Madrid" >> $PHP_INI_DIR/conf.d/php.ini \
          && echo "short_open_tag = Off" >> $PHP_INI_DIR/conf.d/php.ini \
          && echo "memory_limit = 128M" >> $PHP_INI_DIR/conf.d/php.ini  \
          && echo "extension=apcu.so" >> $PHP_INI_DIR/conf.d/php.ini  \
          && echo "apc.enabled=1" >> $PHP_INI_DIR/conf.d/php.ini  \
          && echo "apc.enable_cli=1" >> $PHP_INI_DIR/conf.d/php.ini  \
          && echo "extension=twig.so" >> $PHP_INI_DIR/conf.d/php.ini
