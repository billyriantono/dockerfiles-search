FROM alpine:edge
MAINTAINER Andrew Vityuk <andruwa13@me.com>

RUN echo "@testing http://dl-4.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories
RUN echo "@testing http://nl.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories

ENV DEFAULT_TIMEZONE Europe/Kiev
ENV DEFAULT_PHP_MEMORY_LIMIT 128M
ENV DEFAULT_UPLOAD_MAX_SIZE 100M
ENV DEFAULT_PHP_MAX_FILE_UPLOAD 200
ENV DEFAULT_PHP_MAX_INPUT_VARS 1000
ENV DEFAULT_PHP_MAX_EXECUTION_TIME 60
ENV DEFAULT_PHP_OUTPUT_BUFFERING 4096
ENV DEFAULT_APP_USER nobody
ENV DEFAULT_APP_GROUP nobody

RUN apk add --update nginx bash curl ssmtp git gzip tar nodejs wget ca-certificates && \
    apk add tzdata && \
    apk add --update \
    php5-fpm \
    php5-mcrypt \
    php5-mysqli \
    php5-curl \
    php5-gd \
    php5-json \
    php5-gmp \
    php5-sqlite3 \
    php5-xml \
    php5-zlib \
    php5-openssl \
    php5-pdo \
    php5-zip \
    php5-iconv \
    php5-mysql \
    php5-pgsql \
    php5-opcache \
    php5-posix \
    php5-exif \
    php5-ctype \
    php5-dom \
    php5-phar \
    php5-bcmath \
    php5-pdo_pgsql \
    php5-pdo_mysql \
    php5-pdo_sqlite && \
    sed -i "s|date.timezone =.*|date.timezone = ${DEFAULT_TIMEZONE}|" /etc/php5/php.ini && \
    sed -i "s|memory_limit =.*|memory_limit = ${DEFAULT_PHP_MEMORY_LIMIT}|" /etc/php5/php.ini && \
    sed -i "s|output_buffering =.*|output_buffering = ${DEFAULT_PHP_OUTPUT_BUFFERING}|" /etc/php5/php.ini && \
    sed -i "s|upload_max_filesize =.*|upload_max_filesize = ${DEFAULT_UPLOAD_MAX_SIZE}|" /etc/php5/php.ini && \
    sed -i "s|max_execution_time =.*|max_execution_time = ${DEFAULT_PHP_MAX_EXECUTION_TIME}|" /etc/php5/php.ini && \
    sed -i "s|max_file_uploads =.*|max_file_uploads = ${DEFAULT_PHP_MAX_FILE_UPLOAD}|" /etc/php5/php.ini && \
    sed -i "s|post_max_size =.*|post_max_size = ${DEFAULT_UPLOAD_MAX_SIZE}|" /etc/php5/php.ini && \
    sed -i "s|; max_input_vars =.*|max_input_vars = ${DEFAULT_PHP_MAX_INPUT_VARS}|" /etc/php5/php.ini && \
    sed -i "s|expose_php.*|expose_php = Off|" /etc/php5/php.ini && \
    sed -i "s|short_open_tag.*|short_open_tag = On|" /etc/php5/php.ini && \
    sed -i "s|;sendmail_path =.*|sendmail_path = /usr/sbin/ssmtp -t|" /etc/php5/php.ini && \
    sed -i "s/; cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/" /etc/php5/php.ini && \
    sed -i -e 's/worker_processes\s*1;/worker_processes  auto;/g' /etc/nginx/nginx.conf && \
    cp /usr/share/zoneinfo/${DEFAULT_TIMEZONE} /etc/localtime && \
    echo "${DEFAULT_TIMEZONE}" > /etc/timezone && \
    apk del tzdata && \
    rm -rf /var/cache/apk/*

RUN ln -sf /dev/stdout /var/log/nginx/access.log && \
    ln -sf /dev/stderr /var/log/nginx/error.log && \
    ln -sf /dev/stdout /var/log/fpm-access.log && \
    ln -sf /dev/stderr /var/log/fpm-error.log


COPY files /
ADD ssmtp.conf /etc/ssmtp/ssmtp.conf
ADD boot.sh /boot.sh
RUN chmod 770 /boot.sh

EXPOSE 80

ENTRYPOINT ["/boot.sh"]
