FROM catatnight/postfix

ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8

RUN apt-get update

RUN apt-get install -y python-software-properties && apt install -y software-properties-common
RUN add-apt-repository ppa:ondrej/php

RUN apt-get update && \
    apt-get install -y php-cli php-dev php-curl php-mbstring php-mailparse libmcrypt-dev libreadline-dev git

RUN apt-get -y install gcc g++ make autoconf libc-dev pkg-config

RUN apt-get install php-pear

RUN echo "#define HAVE_MBSTRING 1" >> /usr/include/php/20180731/ext/mbstring/libmbfl/mbfl/mbfilter.h

RUN pecl install mailparse

RUN echo "extension=mailparse.so" >> /etc/php/7.3/cli/php.ini

RUN pecl install --nodeps mcrypt-snapshot

RUN echo "extension=mcrypt.so" >> /etc/php/7.3/cli/php.ini

# install composer
RUN curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer && \
    chmod 755 /usr/local/bin/composer

WORKDIR /etc/postfix

RUN composer require php-mime-mail-parser/php-mime-mail-parser
