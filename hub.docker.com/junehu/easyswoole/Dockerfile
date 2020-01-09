# 从官方基础版本构建
ARG PHP_VERSION=7.3.10
FROM php:${PHP_VERSION}-alpine

# easyswoole的版本
ARG EASYSWOOLE_VERSION=3.3.4
# swoole的版本
ARG SWOOLE_VERSION=4.4.13

# 更新为国内的镜像
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories

# 时区
ARG TZ=Asia/Shanghai
# 设置时区
RUN apk add --no-cache tzdata \
    && cp "/usr/share/zoneinfo/${TZ}" /etc/localtime \
    && echo "${TZ}" > /etc/timezone

# 先安装依赖
RUN apk add --no-cache $PHPIZE_DEPS libpng libpng-dev gettext gettext-dev openssl-dev libzip libzip-dev libmcrypt libmcrypt-dev

# bcmath, calendar, gettext, sockets, opcache, gd, zip
# mysqli, pcntl, pdo_mysql, shmop, sysvmsg, sysvsem, sysvshm 扩展
RUN docker-php-ext-install -j$(nproc) mysqli pdo_mysql sockets gd gettext pcntl opcache shmop bcmath zip sysvmsg sysvsem sysvshm calendar

# mcrypt扩展
RUN pecl install mcrypt-1.0.2 && docker-php-ext-enable mcrypt

# redis扩展
RUN pecl install redis-5.0.0 && docker-php-ext-enable redis

# swoole扩展
RUN pecl install swoole-${SWOOLE_VERSION} && docker-php-ext-enable swoole

# 安装inotify扩展
RUN pecl install inotify && docker-php-ext-enable inotify

# 安装 composer
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/ \
    && composer self-update --clean-backups

# 进入工作目录
WORKDIR /var/www/easyswoole

# 安装easyswoole
RUN composer require easyswoole/easyswoole=${EASYSWOOLE_VERSION}

RUN php vendor/bin/easyswoole install

# 指定监听端口
EXPOSE 9501

# 运行容器时执行命令
CMD sh -c 'php easyswoole start -d'
