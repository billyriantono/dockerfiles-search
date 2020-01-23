FROM php:cli

# install and cleanup
RUN apt-get update && apt-get -y install sudo zip git && \
    apt-get -y clean && apt-get -y purge && rm -rf /var/lib/apt/lists/*

# install composer
RUN php -r "readfile('https://getcomposer.org/installer');" > composer-setup.php && \
    php composer-setup.php --filename=composer --install-dir=/bin && \
    rm -f composer-setup.php

# create local user to map in as UID of /opt
RUN adduser --disabled-password --home /home/php  --gecos "" php && \
    chown php:php -R /home/php

WORKDIR /opt

ENV COMPOSER_ALLOW_SUPERUSER 1

RUN curl -sSf https://yake.amsdard.io/install.sh | sudo -E bash

# run php user as local
COPY ./entrypoint.sh /
ENTRYPOINT ["/entrypoint.sh"]
