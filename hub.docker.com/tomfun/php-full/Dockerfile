FROM php:7.1

RUN docker-php-ext-install pdo_mysql
RUN apt-get update -yqq && \
    apt-get install git -yqq && \
    apt-get install zip unzip -yqq

ADD composer.sh /tmp/install_composer.sh
RUN /tmp/install_composer.sh

RUN composer global require squizlabs/php_codesniffer=2.* && \
    composer global require escapestudios/symfony2-coding-standard=* && \
    /root/.composer/vendor/bin/phpcs --config-set installed_paths /root/.composer/vendor/escapestudios/symfony2-coding-standard

ADD xdebug.sh /tmp/install_xdebug.sh
RUN /tmp/install_xdebug.sh
