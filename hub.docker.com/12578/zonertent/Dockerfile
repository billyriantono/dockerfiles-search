FROM ubuntu:16.04

RUN apt update && \
    apt install -y openssh-client wget curl git zip php php-dev php-cli php-mbstring php-curl php-zip && \
    wget https://getcomposer.org/download/1.4.2/composer.phar && \
    install composer.phar /usr/local/bin/composer
