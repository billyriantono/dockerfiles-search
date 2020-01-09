FROM php:7-cli

RUN rm /etc/apt/preferences.d/no-debian-php
RUN apt-get update && apt-get install -y libxml2-dev jq php-soap php-json && docker-php-ext-install soap

ADD api /work

ENTRYPOINT [ "/work/run.sh" ]
WORKDIR /work