FROM php:5.6.38-fpm
LABEL maintainer="Marcio Maciel <marcio@webjump.com.br>"

RUN apt-get update --fix-missing && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
        msmtp \
        imagemagick \
        libssl-dev \
        libxml2-dev \
        libicu-dev \
        libxslt-dev \
        wget libcurl4-openssl-dev \
        unzip \
        ssh-client git vim \
        gnupg2 \
	librabbitmq-dev \
        libssl-dev \
        apt-utils \
    && rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-install mcrypt bcmath mysql mysqli pdo_mysql mbstring ftp soap zip opcache intl xsl sockets \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd

# Install xdebug and redis
RUN pecl install xdebug-2.5.5 redis-4.1.1 amqp \
    && docker-php-ext-enable xdebug redis amqp \
    && rm -rf /tmp/pear 

# Install blackfire agent
RUN export VERSION=`php -r "echo PHP_MAJOR_VERSION.PHP_MINOR_VERSION;"` \
    && curl -A "Docker" -o /tmp/blackfire-probe.tar.gz -D - -L -s https://blackfire.io/api/v1/releases/probe/php/linux/amd64/${VERSION} \
    && tar zxpf /tmp/blackfire-probe.tar.gz -C /tmp \
    && mv /tmp/blackfire-*.so `php -r "echo ini_get('extension_dir');"`/blackfire.so \
    && docker-php-ext-enable blackfire \
    && rm /tmp/blackfire*

# Installing NodeJS from external resource
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash - && \
    apt-get install -y nodejs

#Installing Grunt
RUN npm install -g grunt-cli

RUN echo "blackfire.agent_socket=\${BLACKFIRE_PORT}" > $PHP_INI_DIR/conf.d/blackfire.ini

# Install modman
RUN wget -nv https://raw.github.com/colinmollenhour/modman/master/modman -O /usr/local/bin/modman \
    && chmod +x /usr/local/bin/modman

# Install generate-modnam
RUN wget -nv https://raw.github.com/mhauri/generate-modman/master/generate-modman -O /usr/local/bin/modman-generate \
    && chmod +x /usr/local/bin/modman-generate

# Install Magerun
RUN wget -nv https://files.magerun.net/n98-magerun.phar -O /usr/local/bin/n98-magerun \
    && chmod +x /usr/local/bin/n98-magerun \
    && ln -s /usr/local/bin/n98-magerun /usr/local/bin/magerun

# Install Magerun2
RUN wget -nv https://files.magerun.net/n98-magerun2.phar -O /usr/local/bin/n98-magerun2 \
    && chmod +x /usr/local/bin/n98-magerun2 \
    && ln -s /usr/local/bin/n98-magerun2 /usr/local/bin/magerun2

# Install composer
RUN wget -nv https://getcomposer.org/installer -O /tmp/composer-setup.php \
    && php /tmp/composer-setup.php --quiet --install-dir=/usr/local/bin --filename=composer \
    && rm /tmp/composer-setup.php

# Copy config files
COPY conf/php-fpm.conf /usr/local/etc/
COPY conf/php.ini /usr/local/etc/php/

# Enable PHP cli
RUN chmod ugo+rX -R /usr/local/etc/php

ENV PHP_EXTRA_CONFIGURE_ARGS --enable-fpm --with-fpm-user=app --with-fpm-group=app

# Install PHP CodeSniffer
RUN pear install PHP_CodeSniffer
RUN git clone https://github.com/magento-ecg/coding-standard.git /opt/magento-ecg/coding-standard
RUN phpcs --config-set installed_paths /opt/magento-ecg/coding-standard

# Add user and group
RUN groupadd -g 1000 app && \
    useradd -g 1000 -u 1000 -d /data -s /bin/bash app

WORKDIR /data
