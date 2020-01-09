FROM  php:7.1.5-alpine
MAINTAINER Alexis CASSAN <alexis.cassan@gmail.com>

ENV PHPCS_VERSION=3.0.0

RUN apk --no-cache add openssl
RUN wget https://cs.sensiolabs.org/download/php-cs-fixer-v2.phar -O php-cs-fixer
RUN chmod a+x php-cs-fixer
RUN mv php-cs-fixer /usr/local/bin/php-cs-fixer
