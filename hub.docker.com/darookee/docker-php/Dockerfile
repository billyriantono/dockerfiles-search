FROM php:7.0

MAINTAINER nils@uliczka.xyz

RUN apt-get update > /dev/null && apt-get install -yyq libjpeg-dev \
        libpng-dev libsqlite3-dev libmcrypt-dev git unzip libxrender1 \
        libfontconfig1 libpng12-dev libjpeg-dev libbz2-dev > /dev/null && \
        docker-php-ext-configure gd --with-png-dir=/usr \
        --with-jpeg-dir=/usr > /dev/null && pecl install xdebug > /dev/null \
        && docker-php-ext-install bz2 pdo_mysql gd mysqli pdo_sqlite pdo \
        mcrypt iconv zip > /dev/null && docker-php-ext-enable pdo_mysql bz2 \
        gd mysqli pdo_sqlite pdo mcrypt iconv zip && echo \
        "date.timezone = \"Europe/Berlin\"" > /usr/local/etc/php/php.ini && \
        echo "zend_extension=xdebug.so" > /usr/local/etc/php/conf.d/xdebug.ini

RUN curl -Lo /usr/local/bin/phpunit https://phar.phpunit.de/phpunit.phar && \
    curl -Lo /usr/local/bin/composer https://getcomposer.org/composer.phar && \
    curl -Lo /usr/local/bin/phpcpd https://phar.phpunit.de/phpcpd.phar && \
    curl -Lo /usr/local/bin/phploc https://phar.phpunit.de/phploc.phar && \
    curl -Lo /usr/local/bin/phpmd \
    http://static.phpmd.org/php/latest/phpmd.phar && \
    curl -Lo /usr/local/bin/pdepend \
    http://static.pdepend.org/php/latest/pdepend.phar && \
    curl -Lo /usr/local/bin/phpcs \
    https://squizlabs.github.io/PHP_CodeSniffer/phpcs.phar

RUN chmod +x /usr/local/bin/phpunit && \
    chmod +x /usr/local/bin/composer && \
    chmod +x /usr/local/bin/phpcpd && \
    chmod +x /usr/local/bin/phploc && \
    chmod +x /usr/local/bin/phpmd && \
    chmod +x /usr/local/bin/pdepend && \
    chmod +x /usr/local/bin/phpcs

RUN mkdir /phpcs && git clone \
    git://github.com/escapestudios/Symfony2-coding-standard.git \
    /phpcs/symfony2 && phpcs --config-set installed_paths /phpcs/symfony2
