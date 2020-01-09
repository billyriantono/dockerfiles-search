FROM alpine:edge

MAINTAINER Kirill Garbar <kirill@iterium.co.uk>

ENV TIMEZONE Europe/London

RUN echo 'http://dl-cdn.alpinelinux.org/alpine/edge/testing' >> /etc/apk/repositories \
    && apk --update upgrade \
    && apk add \
        tzdata \
        runit \
        php7 \
        php7-ctype \
        php7-mbstring \
        php7-openssl \
        php7-fileinfo \
        php7-dom \
        php7-curl \
        php7-fpm \
        php7-cli \
        php7-pdo \
        php7-pdo_mysql \
        php7-mcrypt \
        php7-mysqli \
        php7-opcache \

        # required by composer
        php7-phar \
        php7-json \
        php7-zlib \
        php7-xml \
        php7-tokenizer \
        php7-xmlwriter \

        # this add 30mb to image
        #php7-intl \

        # the rest
        php7-bcmath \
        php7-iconv \
        php7-posix \
        php7-session \
        php7-zip \
        nginx \
    && cp /usr/share/zoneinfo/${TIMEZONE} /etc/localtime \
    && echo "${TIMEZONE}" > /etc/timezone \
    && rm -rf /var/cache/apk/* \
    && { \
      echo '[global]'; \
      echo 'daemonize = no'; \
      echo; \
      echo '[www]'; \
      echo 'user = nginx'; \
      echo 'group = nginx'; \
      echo ''; \
      echo 'listen = /var/run/php7-fpm.sock'; \
      echo 'listen.mode = 0666'; \
      echo ''; \
      echo 'pm = dynamic'; \
      echo 'pm.max_children = 5'; \
      echo 'pm.start_servers = 2'; \
      echo 'pm.min_spare_servers = 1'; \
      echo 'pm.max_spare_servers = 3'; \
      echo 'pm.max_requests = 500'; \
      echo ''; \
      echo 'chdir = /app'; \
      echo ''; \
      echo '; Ensure worker stdout and stderr are sent to the main error log.'; \
      echo 'catch_workers_output = yes'; \
      echo ''; \
      echo 'clear_env = no'; \
    } | tee /etc/php7/php-fpm.d/www.conf \
    && sed -i -e "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/g" /etc/php7/php.ini \
    && sed -i 's/variables_order = "GPCS"/variables_order = "EGPCS"/g' /etc/php7/php.ini \
    && sed -i 's/;daemonize = yes/daemonize = no/g' /etc/php7/php-fpm.conf \
    && sed -i 's/;error_log = log\/php7\/error.log/error_log = \/proc\/self\/fd\/2/g' /etc/php7/php-fpm.conf \
    && mkdir /etc/service/nginx \
    && { \
      echo '#!/bin/sh'; \
      echo 'exec 2>&1'; \
      echo 'source /env'; \
      echo 'mkdir -p /run/nginx'; \
      echo 'exec /usr/sbin/nginx -c /etc/nginx/nginx.conf  -g "daemon off;"'; \
    } | tee /etc/service/nginx/run \
    && chmod +x /etc/service/nginx/run \
    && mkdir /etc/service/php7-fpm \
    && { \
      echo '#!/bin/sh'; \
      echo 'exec 2>&1'; \
      echo 'source /env'; \
      echo 'mkdir -p /run/php'; \
      echo 'exec /usr/sbin/php-fpm7 --nodaemonize'; \
    } | tee /etc/service/php7-fpm/run \
    && chmod +x /etc/service/php7-fpm/run \
    # forward request and error logs to docker log collector
    && ln -sf /dev/stdout /var/log/nginx/access.log \
    && ln -sf /dev/stderr /var/log/nginx/error.log

ADD nginx/default.conf /etc/nginx/conf.d/default.conf
ADD runit/runit-wrapper /sbin/

WORKDIR /app

# Install Composer
ONBUILD ARG GITHUB_OAUTH_TOKEN

# Install composer global bin
ONBUILD RUN php -r "readfile('https://getcomposer.org/installer');" | php -- --install-dir=/usr/local/bin --filename=composer \
    && composer config -g github-oauth.github.com $GITHUB_OAUTH_TOKEN \
    && composer global require hirak/prestissimo

EXPOSE 80

CMD ["/sbin/runit-wrapper"]
