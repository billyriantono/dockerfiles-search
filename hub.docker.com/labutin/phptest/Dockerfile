FROM php:5.6

RUN apt-get update && apt-get install -y git \
  && curl -o /usr/local/bin/phpunit https://phar.phpunit.de/phpunit-5.2.12.phar \
  && chmod +x /usr/local/bin/phpunit
