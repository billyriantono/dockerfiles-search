FROM ubuntu:16.04

LABEL authors="theminer3746,namodev"

RUN apt-get update -qq && apt-get upgrade -yqq

# Add package required to add command add-apt-repository
RUN apt-get install -yqq --no-install-recommends apt-utils

# Add command add-apt-repository
RUN apt-get install -yqq \ 
    software-properties-common \
    python-software-properties

# Add php repository
RUN LC_ALL=C.UTF-8 add-apt-repository -y ppa:ondrej/php

# Add public key for php repository (So we can verify the signature)
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 4F4EA0AAE5267A6C

# Inatall the required package(s)
RUN apt-get update -qq && apt-get install -yqq \
    git \
    php7.0 \
    sudo \
    nginx \
    wget \
    curl \
    composer

# Install php packages
RUN apt-get install -yqq \
    php7.0-curl \
    php7.0-json \
    php7.0-mbstring \
    php7.0-xml \
    php7.0-zip \
    php7.0-tokenizer \
    php7.0-pdo \
    php7.0-mongodb
