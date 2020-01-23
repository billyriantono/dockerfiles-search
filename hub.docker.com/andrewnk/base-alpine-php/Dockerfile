FROM php:fpm-alpine

LABEL maintainer="Andrew Kimball"

RUN docker-php-source extract && \
    docker-php-ext-install opcache && \
    docker-php-source delete

RUN addgroup -S nginx && \
    adduser -D -S -h /var/cache/nginx -s /sbin/nologin -G nginx nginx && \
    echo -e 'cgi.fix_pathinfo=0\n \
            post_max_size = 8M\n \
            variables_order= \"GPCS\"\n \
            short_open_tag = Off\n \
            error_reporting = E_ALL & ~E_DEPRECATED & ~E_STRICT\n \
            log_errors = On\n \
            file_uploads = Off\n \
            memory_limit = 128M'\
            >>/usr/local/etc/php/conf.d/docker-vars.ini && \
    sed -i \
        -e "s/;catch_workers_output\s*=\s*yes/catch_workers_output = yes/g" \
        -e "s/pm.max_children = 5/pm.max_children = 4/g" \
        -e "s/pm.start_servers = 2/pm.start_servers = 3/g" \
        -e "s/pm.min_spare_servers = 1/pm.min_spare_servers = 2/g" \
        -e "s/pm.max_spare_servers = 3/pm.max_spare_servers = 4/g" \
        -e "s/;pm.max_requests = 500/pm.max_requests = 200/g" \
        -e "s/user = www-data/user = nginx/g" \
        -e "s/group = www-data/group = nginx/g" \
        -e "s/^;clear_env = no$/clear_env = no/" \
        /usr/local/etc/php-fpm.d/www.conf && \
    echo -e 'opcache.enable=on\n \
            opcache.fast_shutdown=1\n \
            opcache.revalidate_freq=60\n \
            opcache.validate_timestamps=0\n \
            opcache.max_accelerated_files=4000\n \
            opcache.interned_strings_buffer=16\n \
            opcache.memory_consumption=192'\
            >>/usr/local/etc/php/conf.d/opcache-recommended.ini
