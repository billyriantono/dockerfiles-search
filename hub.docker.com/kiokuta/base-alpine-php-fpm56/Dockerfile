# 基于alpine的php5.6版本需要使用alpine3.8基础镜像
# 基于php56-cli版本
FROM kiokuta/base-alpine-php56:latest

LABEL maintainer="stephen@iot-sw.net" \
      license="MIT" \
      org.label-schema.schema-version="1.0.0" \
      org.label-schema.vendor="KIOKUTA" \
      org.label-schema.name="alpine-php56-fpm" \
      org.label-schema.description="small php-fpm56 with gearman extension image based on alpine" \
      org.label-schema.vcs-url="https://github.com/KIOKUTA/base-alpine-php-fpm56"

WORKDIR /data/worker

# 添加对应的应用
RUN apk update \
    && apk add --no-cache \
        php5-fpm \
        php5-gd \
        php5-pdo_mysql \
        php5-curl \
        php5-iconv \
        php5-xml \
        php5-json \
        php5-dom \
        php5-ctype \
        php5-phar \
        php5-sqlite3 \
        php5-apcu \
        php5-openssl \
        php5-bz2 \
        php5-xmlrpc \
        php5-posix \
        php5-mcrypt \
        php5-ftp \
        php5-gettext \
        php5-opcache \        
        nginx \
        && ln -sf /usr/local/lib/php/extensions/no-debug-non-zts-20131226/gearman.so /usr/lib/php5/modules/gearman.so \
        && ln -sf /usr/local/lib/php/extensions/no-debug-non-zts-20131226/redis.so /usr/lib/php5/modules/redis.so \
        && ln -sf /usr/local/etc/php/conf.d/docker-php-ext-gearman.ini /etc/php5/conf.d/gearman.ini \
        && ln -sf /usr/local/etc/php/conf.d/docker-php-ext-redis.ini /etc/php5/conf.d/redis.ini  

# 添加默认配置文件      
COPY ./config/php/php.ini /etc/php5/
COPY ./config/php/php-fpm.conf /etc/php5/
COPY ./config/nginx/nginx.conf /etc/nginx/

# 添加openrc守护进程
RUN apk add --no-cache \
        openrc \
    && sed -i '269s/cgroup_add_service/#cgroup_add_service/g' /lib/rc/sh/openrc-run.sh \
    && sed -i 's/#rc_sys=""/rc_sys="lxc"/g' /etc/rc.conf \
    && echo 'rc_provide="loopback net"' >> /etc/rc.conf \
    && sed -i 's/^#\(rc_logger="YES"\)$/\1/' /etc/rc.conf \
    && sed -i '/tty/d' /etc/inittab \
    && sed -i 's/hostname $opts/# hostname $opts/g' /etc/init.d/hostname \
    && sed -i 's/mount -t tmpfs/# mount -t tmpfs/g' /lib/rc/sh/init.sh \
    # 添加启动项
    && rc-update add nginx default \
    && rc-update add php-fpm default \
    && rm -rf /tmp/pear/* \
    && mkdir -p /usr/lib/php/pear /data/www /var/log/nginx /var/log/php-fpm 

VOLUME ["/data/worker", "/data/log", "/var/log/nginx", "/var/log/php-fpm"]

CMD ["/sbin/init"]

