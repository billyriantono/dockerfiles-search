FROM php:fpm-alpine

MAINTAINER mcheng827@gmail.com

RUN set -xe \
    && apk add --no-cache \
        postgresql-dev

RUN docker-php-ext-install \
    pdo \
    pdo_pgsql \
    pgsql

RUN { \
        echo '[www]'; \
        echo "php_admin_flag[expose_php] = Off"; \
        echo "php_admin_flag[log_errors] = On"; \
        echo "php_admin_flag[display_errors] = Off"; \
        echo "php_admin_flag[allow_url_include] = Off"; \
        echo "php_admin_value[disable_functions] = exec,passthru,shell_exec,system,proc_open,popen,curl_exec,curl_multi_exec,parse_ini_file,show_source"; \
    } | tee /usr/local/etc/php-fpm.d/custom_settings.conf

