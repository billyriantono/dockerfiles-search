FROM ubuntu:latest

ENV	DEBIAN_FRONTEND noninteractive

RUN apt-get update
RUN apt-get install -y --no-install-recommends \
    git \
    php-cli \
    php-mbstring \
    php-gd \
    php-curl \
    php-xml \
    curl \
    ca-certificates \
    openssh-client \
    sshpass \
    mysql-client

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN composer global require --dev lucatume/wp-browser

RUN ln -s /root/.composer/vendor/codeception/codeception/codecept /usr/local/bin/codecept

COPY wait_services.sh /usr/local/bin/
RUN chmod +x /usr/local/bin/wait_services.sh

RUN rm -rf /var/lib/apt/lists/*
