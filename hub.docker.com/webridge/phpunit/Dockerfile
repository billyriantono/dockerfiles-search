# PHPUnit + PostreSQL driver
#
# VERSION 0.0.1

FROM phpunit/phpunit:5.0.3
MAINTAINER Thomas Barthelemy <thomas.barthelemy@webridge.asia>

RUN apt-get update -q && \
    apt-get install php5-pgsql --no-install-recommends -qy && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /var/tmp/*

RUN echo 'extension = /usr/lib/php5/20131226/pdo_pgsql.so' >> /usr/local/etc/php/php.ini
