FROM php:7.2.1-fpm-stretch

LABEL maintainer="Leon <nian0408@foxmail.com>"

COPY ./sources.list /etc/apt/sources.list
COPY ./php.ini /usr/local/etc/php/conf.d/php.ini

RUN apt-get update && apt-get install -y gnupg apt-transport-https procps net-tools lsof vim supervisor; \
    mkdir -p /var/log/supervisor; \
    curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -; \
    curl https://packages.microsoft.com/config/debian/9/prod.list > /etc/apt/sources.list.d/mssql-release.list; \
    apt-get update; \
    apt-get install -y --no-install-recommends libfreetype6-dev libjpeg62-turbo-dev zlib1g-dev libpng-dev; \
    ACCEPT_EULA=Y apt-get install -y --no-install-recommends msodbcsql17; \
    ACCEPT_EULA=Y apt-get install -y --no-install-r\ecommends mssql-tools; \
    ACCEPT_EULA=Y apt-get install -y --no-install-recommends unixodbc-dev; \
    \
    curl -fsSL 'https://github.com/edenhill/librdkafka/archive/v1.0.0-RC8-test-deps11.tar.gz' -o librdkafka.tar.gz \
    && mkdir -p librdkafka \
    && tar -xf librdkafka.tar.gz -C librdkafka --strip-components=1 \
    && rm librdkafka.tar.gz \
    && ( \
        cd librdkafka \
        && ./configure \
        && make -j "$(nproc)" \
        && make install \
    ) \
    && rm -r librdkafka; \
    docker-php-ext-install pdo gd mysqli pdo_mysql zip; \
    pecl channel-update pecl.php.net; \
    pecl install redis rdkafka pdo_sqlsrv sqlsrv; \
    \
    docker-php-ext-enable redis rdkafka gd mysqli pdo_mysql pdo_sqlsrv sqlsrv; \
    \
    rm -rf /var/lib/apt/lists/*; \
    apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false; \
    sed -i "s/clear_env = no/clear_env = yes/g" /usr/local/etc/php-fpm.d/docker.conf; \
    echo "php_flag[display_errors] = on" >> /usr/local/etc/php-fpm.d/www.conf; \
    echo "php_admin_value[memory_limit] = 128M" >> /usr/local/etc/php-fpm.d/www.conf; \
    echo "php_admin_flag[log_errors] = on" >> /usr/local/etc/php-fpm.d/www.conf;

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

EXPOSE 9000
CMD ["/usr/bin/supervisord"]