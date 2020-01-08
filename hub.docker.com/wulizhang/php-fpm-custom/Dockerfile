# 基于官方PHP最新稳定且安全镜像自定义扩展(制作日期2019/6/13)
FROM php:7.2-fpm

LABEL main contrib maintainer="WuliZhang"

# 系统源替换为清华大学镜像站
RUN mv /etc/apt/sources.list /etc/apt/sources.list.bak && \
        echo "deb http://mirrors.tuna.tsinghua.edu.cn/debian/ stretch main contrib non-free" >> /etc/apt/sources.list && \
        echo "# deb-src http://mirrors.tuna.tsinghua.edu.cn/debian/ stretch main contrib non-free" >> /etc/apt/sources.list && \
        echo "deb http://mirrors.tuna.tsinghua.edu.cn/debian/ stretch-updates main contrib non-free" >> /etc/apt/sources.list && \
        echo "# deb-src http://mirrors.tuna.tsinghua.edu.cn/debian/ stretch-updates main contrib non-free" >> /etc/apt/sources.list && \
        echo "deb http://mirrors.tuna.tsinghua.edu.cn/debian/ stretch-backports main contrib non-free" >> /etc/apt/sources.list && \
        echo "# deb-src http://mirrors.tuna.tsinghua.edu.cn/debian/ stretch-backports main contrib non-free" >> /etc/apt/sources.list && \
        echo "deb http://mirrors.tuna.tsinghua.edu.cn/debian-security stretch/updates main contrib non-free" >> /etc/apt/sources.list && \
        echo "# deb-src http://mirrors.tuna.tsinghua.edu.cn/debian-security stretch/updates main contrib non-free" >> /etc/apt/sources.list

RUN apt-get update \
        && apt-get install -y unzip wget sudo libpng-dev libjpeg-dev libbz2-dev libicu-dev libmcrypt-dev libpq-dev libmagickwand-dev \
        && rm -rf /var/lib/apt/lists/*

# 安装PHP扩展
RUN docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr \
        && docker-php-ext-install bcmath \
        bz2 \
        exif \
        gettext \
        gd \
        intl \
        opcache \
        pcntl \
        pdo_mysql \
        pdo_pgsql \
        pgsql \
        soap \
        sockets \
        zip

RUN pecl install Imagick && echo "extension=imagick.so" > /usr/local/etc/php/conf.d/imagick.ini
RUN pecl install mcrypt-1.0.1 && echo "extension=mcrypt.so" > /usr/local/etc/php/conf.d/mcrypt.ini

RUN chmod g+w /usr/local/etc/php/conf.d/ \
        && usermod -a -G staff www-data \
        && chown www-data:staff /var/www \
        && echo 'www-data  ALL=(ALL:ALL) NOPASSWD: ALL' > /etc/sudoers.d/www-data

USER www-data
WORKDIR /var/www
