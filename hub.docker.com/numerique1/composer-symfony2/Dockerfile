FROM ubuntu:12.04

MAINTAINER Kévin Lysiak <kevin.lysiak@numerique1.fr>

RUN apt-get update -qq
RUN apt-get install -qqy php5-cli php5-intl curl

# install composer
RUN curl -sS https://getcomposer.org/installer | php

VOLUME ["/srv"]
WORKDIR /srv
ENTRYPOINT ["/composer.phar"]
