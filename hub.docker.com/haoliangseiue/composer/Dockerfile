FROM composer:latest

# 加速网络传输
RUN composer config -g repo.packagist composer https://packagist.phpcomposer.com \
        && rm -rf /tmp/*

RUN apk add --no-cache tzdata \
    && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
