FROM debian:stretch-slim
MAINTAINER victor apostol <apostol.victor@gmail.com>
ENV LAST_UPDATED 2019-05-07
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update
RUN apt-get -y upgrade
RUN apt-get install -y wget curl apt-transport-https lsb-release ca-certificates sudo gnupg2
RUN wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
RUN echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" | tee /etc/apt/sources.list.d/php.list
RUN curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
RUN apt-get update
RUN apt-get update && apt-get install -y php7.2-cli php7.2-mysql php7.2-curl php7.2-gd php7.2-mbstring php7.2-zip php7.2-xml php7.2-sqlite 
RUN apt-get install -y php7.2-soap nodejs libpng-dev git zip unzip

RUN apt-get clean -y && apt-get autoclean -y && apt-get autoremove -y && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN mkdir -p /run/php

RUN curl -o /tmp/composer-setup.php https://getcomposer.org/installer \
  && curl -o /tmp/composer-setup.sig https://composer.github.io/installer.sig \
  && php -r "if (hash('SHA384', file_get_contents('/tmp/composer-setup.php')) !== trim(file_get_contents('/tmp/composer-setup.sig'))) { unlink('/tmp/composer-setup.php'); echo 'Invalid installer' . PHP_EOL; exit(1); }"
ENV COMPOSER_VERSION 1.8.5

# Install Composer
RUN php /tmp/composer-setup.php --no-ansi --install-dir=/usr/local/bin --filename=composer --version=${COMPOSER_VERSION} && rm -rf /tmp/composer-setup.php
RUN composer global require "hirak/prestissimo:^0.3"

EXPOSE 9000

CMD ["php-fpm7.2", "-F"]
