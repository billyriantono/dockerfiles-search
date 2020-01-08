FROM php:7.3-fpm-stretch

ENV ImageDeps="\
    cron \
    default-mysql-client \
    git \
"

# Install PHP7
RUN buildDeps=" \
        libpng-dev \
        libjpeg-dev \
        libmcrypt-dev \
        libxml2-dev \
        freetype* \
        libxslt1-dev \
        cron \
        libicu-dev \
        libfreetype6-dev \
        libzip-dev \
    "; \
    set -x \
    && apt-get update && apt-get install -y $ImageDeps $buildDeps --no-install-recommends \
    && rm -rf /var/lib/apt/lists/*
RUN docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr --with-freetype-dir=/usr \
    && docker-php-ext-install -j "$(getconf _NPROCESSORS_ONLN)" \
    gd \
    mbstring \
    mysqli \
    pdo_mysql \
    soap \
    zip \
    bcmath \
    intl \
    xsl \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install Tools
RUN apt-get update && \
    apt-get install -y \
    vim \
    zip  \
    bzip2 \
    jq \
    mysql-client \
    git-core \
    && apt-get purge -y --auto-remove

# Install SSH
RUN apt-get update && apt-get install -y openssh-server

#Install sudo
RUN apt-get update && apt-get install sudo

# Add magento user, make it sudo and sudo without passwd
RUN useradd -m magento && echo "magento:magento" | chpasswd && adduser magento sudo \
    && usermod -g www-data magento
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

USER magento
WORKDIR /home/magento