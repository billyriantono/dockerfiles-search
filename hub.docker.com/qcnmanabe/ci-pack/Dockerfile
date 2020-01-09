FROM alpine:latest

# Refs. https://github.com/codecasts/php-alpine
#
# trust this project public key to trust the packages.
ADD https://php.codecasts.rocks/php-alpine.rsa.pub /etc/apk/keys/php-alpine.rsa.pub
RUN echo "@php https://php.codecasts.rocks/v3.7/php-7.2" >> /etc/apk/repositories

RUN apk add --update \
    coreutils \
    bash \
    build-base \
    libffi-dev \
    python-dev \
    openssl-dev \
    openssh-client \
    curl \
    git \
    jq \
    tzdata \
    py-pip \
    php@php \
    php-mbstring@php \
    php-phar@php \
    php-zlib@php \
    php-json@php \
    php-ctype@php

RUN ln -s /usr/bin/php7 /usr/bin/php

# set up timezone
RUN cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime && \
    echo "Asia/Tokyo" > /etc/timezone && \
    rm -rf /var/cache/apk/*

# Install ansible
RUN pip install --upgrade pip
RUN pip install ansible

# Install aws-cli
RUN pip install awscli

# Install Deployer
RUN curl -LO https://deployer.org/deployer.phar
RUN mv deployer.phar /usr/local/bin/dep
RUN chmod +x /usr/local/bin/dep

