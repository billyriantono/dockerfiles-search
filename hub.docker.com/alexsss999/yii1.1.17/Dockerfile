FROM php:7.0.16-fpm
MAINTAINER alex-saf

ENV LANG=en_US.UTF-8 LANGUAGE=en_US:en LC_ALL=en_US.UTF-8 DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
    && apt-get -y install \
            libicu52 \
            libicu-dev \

            # Required by composer
            git \
            zlib1g-dev \
        --no-install-recommends \

    # Required extension
    && docker-php-ext-install -j$(nproc) intl \

    # Additional common extensions
    && docker-php-ext-install -j$(nproc) opcache \
    && docker-php-ext-install bcmath \
    && docker-php-ext-install mysqli && docker-php-ext-install pdo_mysql \
    && pecl install apcu-5.1.8 && docker-php-ext-enable apcu \

    # Required by composer
    && docker-php-ext-install -j$(nproc) zip \

    # Cleanup to keep the images size small
    && apt-get purge -y \
        icu-devtools \
        libicu-dev \
        zlib1g-dev \
    && apt-get autoremove -y \
    && rm -r /var/lib/apt/lists/*

# Install composer
COPY install-composer /install-composer
RUN /install-composer && rm /install-composer && useradd -u 1000 -s /bin/bash -d /home/icons8 icons8

# Install framework yii 1.1.17
#COPY framework /var/www/html/framework
ADD framework.tar.gz /home/icons8
ADD requirements.tar.gz /home/icons8
#RUN chown -R icons8.icons8 /home/icons8

#USER icons8
WORKDIR /home/icons8
#
