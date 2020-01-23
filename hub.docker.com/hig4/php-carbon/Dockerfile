FROM php:7.1-cli-alpine

WORKDIR /tmp

RUN curl https://getcomposer.org/installer | php
RUN php composer.phar require nesbot/carbon

ENTRYPOINT ["php", "-d", "auto_prepend_file=vendor/autoload.php", "-a"]