FROM php:7.0-apache
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

    # Additional common extensions
    && docker-php-ext-install -j$(nproc) intl opcache zip \
    && docker-php-ext-install bcmath mysqli pdo_mysql \
    && pecl install apcu-5.1.8 && docker-php-ext-enable apcu \

    # Cleanup to keep the images size small
    && apt-get purge -y \
        icu-devtools \
        libicu-dev \
        zlib1g-dev \
    && apt-get autoremove -y \
    && rm -r /etc/apache2/sites-enabled/* \
    && rm -r /var/lib/apt/lists/*

RUN useradd -u 1000 -s /bin/bash -d /home/icons8 icons8 \
    && mkdir -p /home/icons8/blog.icons8.com/web \
    && mkdir -p /home/icons8/logs/blog.icons8.com \
    && ln -s /etc/apache2/mods-available/rewrite.load /etc/apache2/mods-enabled/rewrite.load

# Install Apache config's
COPY ports.conf /etc/apache2/
COPY blog.icons8.com.apache.conf /etc/apache2/sites-enabled/

# Install blog
#COPY blog.tar.gz /home/icons8/blog.icons8.com
#ADD blog.tar.gz /home/icons8
#RUN chown -R icons8.icons8 /home/icons8

EXPOSE 8000

#USER icons8
WORKDIR /home/icons8
#
