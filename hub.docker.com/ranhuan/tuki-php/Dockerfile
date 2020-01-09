FROM php:7.1-fpm
RUN apt-get update \
    && apt-get install -y \
        libmcrypt-dev \
        libmemcached-dev \
        zlib1g-dev \
        libz-dev \
        git \
        wget \
        libpcre3-dev \
    && docker-php-ext-install \
        mcrypt \
        mbstring \
        pdo_mysql \
        gettext \
        zip \
    && pecl install memcached \
    && docker-php-ext-enable memcached \
    # 用完包管理器后安排打扫卫生可以显著的减少镜像大小
    && apt-get clean \
    && apt-get autoclean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    # 安装 Composer，此物是 PHP 用来管理依赖关系的工具
    && curl -sS https://getcomposer.org/installer \
        | php -- --install-dir=/usr/local/bin --filename=composer