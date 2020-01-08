FROM alpine:latest
LABEL maintainer "DI GREGORIO Nicolas <nicolas.digregorio@gmail.com>"

### Environment variables
ENV LANG='en_US.UTF-8' \
    LANGUAGE='en_US.UTF-8' \
    TERM='xterm' \
    TIMEZONE='Europe/Brussels' \
    PHP_MEMORY_LIMIT='2048M' \
    MAX_UPLOAD='50' \
    PHP_MAX_FILE_UPLOAD='2048M' \
    PHP_MAX_POST='2048M' \ 
    FPM_PM='dynamic' \
    FPM_PM_MAX_CHILDREN='20' \
    FPM_PM_START_SERVERS='3' \
    FPM_PM_MIN_SPARE_SERVERS='2' \
    FPM_PM_MAX_SPARE_SERVERS='5' \
    FPM_PM_MAX_REQUESTS='1000' \ 
    PHP_MBSTRING_HTTP_INPUT='pass' \
    PHP_MBSTRING_HTTP_OUTPUT='pass' \ 
    PHP_CGI_FIX_INFOPATH='1' \
    PHP_ENV_PATH='/usr/local/bin:/usr/bin:/bin' \
    PHP_RAW_POST_DATA='-1' \
    OPCACHE_ENABLE='1' \
    OPCACHE_ENABLE_CLI='1' \
    OPCACHE_INTERNED_STRINGS_BUFFER='8' \
    OPCACHE_MAX_ACCELERATED_FILES='10000' \
    OPCACHE_MEMORY_CONSUMPTION='128' \
    OPCACHE_SAVE_COMMENTS='1' \
    OPCACHE_REVALIDATE_FREQ='1'

### Install Application
RUN apk upgrade --no-cache && \
    apk add --no-cache --virtual=run-deps \
      su-exec \
      ssmtp \
      php7-apcu \
      php7-bcmath \
      php7-bz2 \
      php7-ctype \
      php7-curl \
      php7-dom \ 
      php7-fileinfo \
      php7-ftp \
      php7-gd \
      php7-gettext \
      php7-iconv \
      php7-intl \
      php7-json \
      php7-mbstring \
      php7-mcrypt \
      php7-memcached \
      php7-mysqlnd \
      php7-mysqli \
      php7-odbc \
      php7-opcache \
      php7-openssl \
      php7-pcntl \
      php7-pdo \
      php7-pdo_dblib \
      php7-pdo_odbc \
      php7-pdo_mysql \
      php7-pdo_pgsql \
      php7-pdo_sqlite \
      php7-phar \
      php7-pgsql \
      php7-posix \
      php7-soap \
      php7-sqlite3 \
      php7-simplexml \
      php7-xmlreader \
      php7-xmlrpc \
      php7-xmlwriter \
      php7-zip \
      php7-zlib \
      php7-fpm && \
    sed -i "s|;*daemonize\s*=\s*yes|daemonize = no|g" /etc/php7/php-fpm.conf && \
    sed -i "s|;*env\[PATH\].*=.*/usr/local/bin:/usr/bin:/bin|env\[PATH\] = ${PHP_ENV_PATH}|g" /etc/php7/php-fpm.d/www.conf && \
    sed -i "s|;*listen\s*=\s*127.0.0.1:9000|listen = 9000|g" /etc/php7/php-fpm.d/www.conf && \
    sed -i "s|;*listen\s*=\s*/||g" /etc/php7/php-fpm.d/www.conf && \
    sed -i "s|;*error_log\s*=\s*/var/log/php-fpm.log|error_log = /var/log/php7/error.log|g" /etc/php7/php-fpm.conf && \
    sed -i "s|;*date.timezone =.*|date.timezone = ${TIMEZONE}|i" /etc/php7/php.ini && \
    sed -i "s|;*memory_limit =.*|memory_limit = ${PHP_MEMORY_LIMIT}|i" /etc/php7/php.ini && \
    sed -i "s|;*upload_max_filesize =.*|upload_max_filesize = ${PHP_MAX_FILE_UPLOAD}|i" /etc/php7/php.ini && \
    sed -i "s|;*max_file_uploads =.*|max_file_uploads = ${MAX_UPLOAD}|i" /etc/php7/php.ini && \
    sed -i "s|;*post_max_size =.*|post_max_size = ${PHP_MAX_POST}|i" /etc/php7/php.ini && \
    sed -i "s|;*mbstring.http_input =.*|mbstring.http_input = ${PHP_MBSTRING_HTTP_INPUT}|i" /etc/php7/php.ini && \
    sed -i "s|;*mbstring.http_output =.*|mbstring.http_output = ${PHP_MBSTRING_HTTP_OUTPUT}|i" /etc/php7/php.ini && \
    sed -i "s|;*cgi.fix_pathinfo.*=.*|cgi.fix_pathinfo = ${PHP_CGI_FIX_INFOPATH}|i" /etc/php7/php.ini && \
    sed -i "s|;always_populate_raw_post_data.*=.*|always_populate_raw_post_data = ${PHP_RAW_POST_DATA}|i" /etc/php7/php.ini && \
    sed -i "s|pm =.*|pm = ${FPM_PM}|i" /etc/php7/php-fpm.d/www.conf && \
    sed -i "s|pm.max_children =.*|pm.max_children = ${FPM_PM_MAX_CHILDREN}|i" /etc/php7/php-fpm.d/www.conf && \
    sed -i "s|pm.start_servers =.*|pm.start_servers = ${FPM_PM_START_SERVERS}|i" /etc/php7/php-fpm.d/www.conf && \
    sed -i "s|pm.min_spare_servers =.*|pm.min_spare_servers = ${FPM_PM_MIN_SPARE_SERVERS}|i" /etc/php7/php-fpm.d/www.conf && \
    sed -i "s|pm.max_spare_servers =.*|pm.max_spare_servers = ${FPM_PM_MAX_SPARE_SERVERS}|i" /etc/php7/php-fpm.d/www.conf && \
    sed -i "s|pm.max_requests =.*|pm.max_requests = ${FPM_PM_MAX_REQUESTS}|i" /etc/php7/php-fpm.d/www.conf && \
    sed -i "s|user =.*|;user = wwwuser|i" /etc/php7/php-fpm.d/www.conf && \
    sed -i "s|group =.*|;group = wwwuser|i" /etc/php7/php-fpm.d/www.conf && \
    sed -i "s|;opcache.enable_cli.*=.*|opcache.enable_cli = ${OPCACHE_ENABLE_CLI}|i" /etc/php7/php.ini && \
    sed -i "s|;opcache.enable.*=.*|opcache.enable = ${OPCACHE_ENABLE}|i" /etc/php7/php.ini && \
    sed -i "s|;opcache.memory_consumption.*=.*|opcache.memory_consumption = ${OPCACHE_MEMORY_CONSUMPTION}|i" /etc/php7/php.ini && \
    sed -i "s|;opcache.interned_strings_buffer.*=.*|opcache.interned_strings_buffer = ${OPCACHE_INTERNED_STRINGS_BUFFER}|i" /etc/php7/php.ini && \
    sed -i "s|;opcache.max_accelerated_files.*=.*|opcache.max_accelerated_files = ${OPCACHE_MAX_ACCELERATED_FILES}|i" /etc/php7/php.ini && \
    sed -i "s|;opcache.revalidate_freq.*=.*|opcache.revalidate_freq = ${OPCACHE_REVALIDATE_FREQ}|i" /etc/php7/php.ini && \
    sed -i "s|;opcache.save_comments.*=.*|opcache.save_comments = ${OPCACHE_SAVE_COMMENTS}|i" /etc/php7/php.ini && \
    php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php --install-dir=/usr/local/bin --filename=composer && \
    php -r "unlink('composer-setup.php');" && \
    echo "include=/etc/php7/fpm.d/*.conf" >> /etc/php7/php-fpm.conf && \
    rm -rf /tmp/* \
           /var/cache/apk/*  \
           /var/tmp/*
    
# Expose volumes
VOLUME ["/www","/etc/php7/fpm.d","/var/log/php7"]

# Expose ports
EXPOSE 9000

### Running User: not used, managed by docker-entrypoint.sh
#USER wwwuser

### Start php-fpm
COPY ./docker-entrypoint.sh /
ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["php-fpm"]
