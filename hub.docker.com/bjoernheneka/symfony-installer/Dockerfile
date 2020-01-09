FROM php:cli

MAINTAINER Bjoern Heneka <bheneka@codebee.de>

RUN apt-get update \
    && apt-get install -y vim \
    && apt-get clean

RUN mkdir -p /usr/local/bin \
    && curl -LsS https://symfony.com/installer -o /usr/local/bin/symfony \
    && chmod a+x /usr/local/bin/symfony

ENTRYPOINT ["/usr/local/bin/symfony"]