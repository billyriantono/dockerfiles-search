FROM phpstan/phpstan:0.11

RUN apk --no-cache add php7-soap php7-pcntl
RUN composer global require \
    phpstan/phpstan-phpunit:^0.11 \
    phpstan/phpstan-doctrine:^0.11 \
    phpstan/phpstan-symfony:^0.11
