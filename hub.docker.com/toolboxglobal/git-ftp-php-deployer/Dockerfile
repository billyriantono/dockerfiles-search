FROM ubuntu:16.04

LABEL maintainer="<nathan.daly@toolboxmarketing.com>"

ENV DEBIAN_FRONTEND noninteractive

# Install required packages
RUN apt-get update && apt-get install -y software-properties-common \
    php7.0-cli software-properties-common git-ftp unzip
RUN add-apt-repository ppa:git-ftp/ppa && apt-get update && apt-get install -y git-ftp

# Install compopser
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Slim down the image
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/man/?? /usr/share/man/??_*
