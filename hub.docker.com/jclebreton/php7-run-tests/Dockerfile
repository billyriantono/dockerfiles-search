FROM php:7-cli

MAINTAINER Jean-Christophe Lebreton <jclebreton@gmail.com>

RUN cd /tmp/ && \
    curl -O https://pecl.php.net/get/apcu-5.1.3.tgz && \
    tar zxvf apcu-5.1.3.tgz && \
    mv apcu-5.1.3 /usr/src/php/ext/apcu \
    && docker-php-ext-install -j $(nproc) apcu

RUN cd /tmp/ && \
    curl -O https://pecl.php.net/get/apcu_bc-1.0.3.tgz && \
    tar zxvf apcu_bc-1.0.3.tgz && \
    mv apcu_bc-1.0.3 /usr/src/php/ext/apcu \
    && docker-php-ext-install -j $(nproc) apcu

RUN echo "apc.enable_cli=1" >> /usr/local/etc/php/conf.d/docker-php-ext-apcu.ini

RUN curl https://getcomposer.org/download/1.0.0-alpha11/composer.phar -o /usr/local/bin/composer &&\
    chmod +x /usr/local/bin/composer

RUN curl https://phar.phpunit.de/phpunit-5.1.3.phar -o /usr/local/bin/phpunit &&\
    chmod +x /usr/local/bin/phpunit

RUN curl http://get.sensiolabs.org/sami.phar -o /usr/local/bin/sami &&\
    chmod +x /usr/local/bin/sami

RUN curl http://get.sensiolabs.org/php-cs-fixer.phar -o /usr/local/bin/php-cs-fixer &&\
    chmod +x /usr/local/bin/php-cs-fixer

RUN mkdir -p /root/php/
WORKDIR /root/php/

CMD [ "phpunit" ]
