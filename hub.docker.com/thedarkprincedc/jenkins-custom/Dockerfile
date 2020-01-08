FROM jenkins/jenkins:2.125-alpine
MAINTAINER FAN ZHI SHEN <thedarkprincedc@yahoo.com>
LABEL Description="This is a jenkins docker image with nodejs, grunt, and electron" Vendor="thedarkprincedc" Version="1.0"
USER root
RUN apk update && \
    apk add nodejs && \
    apk add php7 php7-dom php7-xml php7-curl php7-pdo php7-pdo_mysql php7-json php7-phar php7-iconv php7-mbstring && \
    npm install -g grunt-cli && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN curl -sSL https://phar.phpunit.de/phpunit.phar -o phpunit.phar && \
    chmod +x phpunit.phar && \
    mv phpunit.phar /usr/local/bin/phpunit && \
    rm -fr /var/cache/apk/*
USER jenkins