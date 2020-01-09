FROM sumsai/p7:latest

ENV APP_ROOT /var/www/frame

WORKDIR $APP_ROOT

# RUN sed 's/archive.ubuntu.com/mirrors.aliyun.com/' -i.bak /etc/apt/sources.list && apt-get update -y

RUN DEBIAN_FRONTEND="noninteractive" \
    && yum update -y \
    && yum install -y zip \
    && useradd www && chown -R www:www $APP_ROOT \
    && mkdir -p /var/www && chown -R www:www /var/www \
    && HOME=/var/www USER=www su -p -s /bin/sh -c "composer config -g repo.packagist composer https://packagist.phpcomposer.com && composer create-project topthink/think $APP_ROOT --prefer-dist" www \
    && yum clean packages \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /var/www/.composer/cache
    WORKDIR /frame
CMD su -p -s /bin/sh -c "php -S 0.0.0.0:8000 -t $APP_ROOT/public" www
