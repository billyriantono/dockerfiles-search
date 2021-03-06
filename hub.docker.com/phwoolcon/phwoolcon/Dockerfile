FROM alpine:3.9

ARG ALPINE_REPO=""
ARG UTILS_BASE="https://raw.githubusercontent.com/phwoolcon/docker-utils/master"
ENV ENV="/etc/profile"
RUN wget ${UTILS_BASE}/alpine/aliases.sh -O /etc/profile.d/aliases.sh; \
    wget ${UTILS_BASE}/alpine/pick-mirror -O /usr/local/bin/pick-mirror; \
    wget ${UTILS_BASE}/alpine/determine-fpm-workers -O /usr/local/bin/determine-fpm-workers; \
    chmod +x /usr/local/bin/*; \
    pick-mirror v3.9; \
    apk update; apk upgrade; \
    apk add --no-cache bash coreutils nginx\
    php7 php7-curl php7-ctype php7-fileinfo php7-fpm php7-gd php7-json php7-mbstring php7-opcache php7-openssl php7-posix \
    php7-pdo php7-pdo_mysql php7-pecl-redis php7-phalcon php7-simplexml php7-sodium php7-tokenizer php7-xml php7-zip \
    composer;
RUN mkdir -p /mnt/data /run/nginx; \
    wget ${UTILS_BASE}/alpine/nginx/00-log-formats.conf -O /etc/nginx/conf.d/00-log-formats.conf; \
    wget ${UTILS_BASE}/alpine/nginx/01-behind-proxy.conf -O /etc/nginx/conf.d/01-behind-proxy.conf; \
    wget ${UTILS_BASE}/alpine/nginx/default.conf -O /etc/nginx/conf.d/default.conf; \
    sed -i 's|/var/log|/mnt/data/log|g' /etc/nginx/nginx.conf; \
    printf "" > /start.sh;
RUN echo 'error_log = /mnt/data/log/php7/error.log' > /etc/php7/php-fpm.d/00-log.conf; \
    sed -i 's|expose_php = On|expose_php = Off|g' /etc/php7/php.ini; \
    sed -i 's|/var/log|/mnt/data/log|g; s|127.0.0.1:9000|0.0.0.0:9000|g; s|pm = dynamic|pm = static|g' \
    /etc/php7/php-fpm.d/www.conf; \
    printf "#!/usr/bin/env bash\n\
[ -f /before-entrypoint ] && /before-entrypoint;\n\
determine-fpm-workers;\n\
[ -f /srv/http/bin/dump-autoload ] && {\n\
    mkdir -p /mnt/data/{config,log/php7,log/app,log/nginx};\n\
    cd /srv/http;\n\
    mkdir -p app/config/production storage/{cache,session} public/{assets,static,uploads};\n\
    ls /mnt/data/config/*.php > /dev/null 2>&1 && ln -snf /mnt/data/config/*.php app/config/production/;\n\
    ln -snf /mnt/data/log/app storage/logs;\n\
    bin/dump-autoload > /dev/null;\n\
    bin/cli migrate:up;\n\
    bin/dump-autoload;\n\
    chown -R nobody:nobody storage/ public/{static,uploads} /mnt/data/log/app;\n\
    [ -f /before-service ] && /before-service;\n\
}\n\
php-fpm7 -D;\n\
nginx -g 'daemon off;'\n" > /entrypoint.sh; \
    chmod +x /entrypoint.sh;
VOLUME /mnt/data
EXPOSE 80 9000
ENTRYPOINT ["/entrypoint.sh"]
