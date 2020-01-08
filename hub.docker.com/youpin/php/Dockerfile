#
# PHP Dockerfile
# version 1.1
#
FROM youpin/ubuntu
MAINTAINER Leo <jiangwenhua@yoyohr.com>

VOLUME /home/data

RUN apt-get update \
    && DEBIAN_FRONTEND="noninteractive" \
        apt-get install -y php7.0-fpm \
        php7.0-bcmath \
        php7.0-curl \
        php7.0-gd \
        php7.0-mbstring \
        php7.0-mysql \
        php7.0-soap \
        php7.0-xml \
        php7.0-zip \    
        --no-install-recommends \
    && mkdir /run/php \
    && rm -rf /var/lib/apt/lists/*

RUN set -ex \
    && cd /etc/php/7.0/fpm \
    && sed -i 's/pm = dynamic/pm = static/g' \
        pool.d/www.conf \
    && sed -i 's/pm.max_children = 5/pm.max_children = 20/g' \
        pool.d/www.conf \
    && { \
        echo '[global]'; \
        echo 'error_log = /proc/self/fd/2'; \
        echo; \
        echo '[www]'; \
        echo '; if we send this to /proc/self/fd/1, it never appears'; \
        echo 'access.log = /proc/self/fd/2'; \
        echo; \
        echo 'clear_env = no'; \
        echo; \
        echo '; Ensure worker stdout and stderr are sent to the main error log.'; \
        echo 'catch_workers_output = yes'; \
    } | tee pool.d/docker.conf \
    && { \
        echo '[global]'; \
        echo 'daemonize = no'; \
        echo; \
        echo '[www]'; \
        echo 'listen = 9000'; \
    } | tee pool.d/zz-docker.conf

EXPOSE 9000
CMD ["php-fpm7.0"]
