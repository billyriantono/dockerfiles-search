FROM daocloud.io/php:5.6-fpm

MAINTAINER wolferhua

# 环境安装
# RUN sed -i 's/deb.debian.org/mirrors.ustc.edu.cn/g' /etc/apt/sources.list \
#     && apt update \
RUN apt update \
    && apt upgrade -y \
    && apt install  -y \
            libfreetype6-dev \
            libmcrypt-dev \
            libjpeg-dev \
            libpng-dev \
            sendmail \
            openssl \
            libpng-dev\
            libssl-dev\
    && apt install zlib1g-dev -y \
    && docker-php-ext-configure gd \
            --enable-gd-native-ttf \
            --with-freetype-dir=/usr/include/freetype2 \
            --with-png-dir=/usr/include \
            --with-jpeg-dir=/usr/include \
    && docker-php-ext-install mbstring zip  gd pdo pdo_mysql mcrypt pcntl mysql mysqli \
    && pecl install redis-4.3.0 \
    && pecl install swoole-1.10.5 \
    && echo "extension=redis.so" > /usr/local/etc/php/conf.d/20-redis.ini \
    && echo "extension=swoole.so" > /usr/local/etc/php/conf.d/20-swoole.ini
    #&& echo "extension=php_pdo_mysql.so" > /usr/local/etc/php/conf.d/20-pdo_mysql.ini
    #&& docker-php-ext-enable redis

RUN sed -i 's/deb.debian.org/mirrors.aliyun.com/g' /etc/apt/sources.list 

ENTRYPOINT ["docker-php-entrypoint"]

# 开放端口
EXPOSE 9000
# 工作目录
WORKDIR /var/www/html

# 运行命令
CMD ["php-fpm"]

# docker build -t wolferhua/php:5.6-fpm .










