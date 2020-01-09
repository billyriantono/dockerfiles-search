FROM debian

MAINTAINER IDCT Bartosz Pachołek <bartosz@idct.pl>

ARG php_version=7.4
# disable interactive functions
ENV DEBIAN_FRONTEND noninteractive

VOLUME ["/code"]

RUN apt-get update
RUN apt-get install -y git wget software-properties-common ca-certificates apt-transport-https gnupg2 zip unzip
RUN wget -O key.txt -q https://packages.sury.org/php/apt.gpg && apt-key add key.txt
RUN echo "deb https://packages.sury.org/php/ buster main" | tee /etc/apt/sources.list.d/php.list | apt-get update

RUN apt-get install -y apt-utils curl php${php_version}-cli php${php_version}-mysqlnd php${php_version}-pgsql php${php_version}-soap php${php_version}-sqlite3 php${php_version}-zip php${php_version}-mysql php${php_version}-redis php${php_version}-intl php${php_version}-imagick php${php_version}-json php${php_version}-gd php${php_version}-curl php${php_version}-xdebug php${php_version}-mbstring php${php_version}-xml && \
rm -rf /var/lib/apt/lists/* && \
cd /tmp && curl -sS https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer

CMD echo "Entering workdir..." && \ 
cd /code && \
echo "Installing..." && \
composer install && \
echo "Running PHPUnit installed by app..." && \
vendor/phpunit/phpunit/phpunit
