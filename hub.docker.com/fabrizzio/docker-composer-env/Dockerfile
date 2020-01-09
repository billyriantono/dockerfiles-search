FROM php:7.0.1-cli
MAINTAINER Dieter Provoost <dieter.provoost@marlon.be>

# install git and enable PHP ZIP extension
RUN apt-get update && apt-get install -y git-core\
        zlib1g-dev \
    && docker-php-ext-install zip



