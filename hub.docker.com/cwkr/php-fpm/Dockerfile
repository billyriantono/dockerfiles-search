FROM php:7.2-fpm-stretch

RUN mv -v "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"
RUN sed -i "s/expose_php = On/expose_php = Off/g" "$PHP_INI_DIR/php.ini"
RUN sed -i "s/memory_limit = 128M/memory_limit = 256M/g" "$PHP_INI_DIR/php.ini"
RUN sed -i "s/upload_max_filesize = 2M/upload_max_filesize = 10M/g" "$PHP_INI_DIR/php.ini"
RUN sed -i "s/disable_functions =/disable_functions = exec,passthru,shell_exec,system,proc_open,proc_close,proc_get_status,proc_nice,proc_terminate,popen,curl_exec,curl_multi_exec/g" "$PHP_INI_DIR/php.ini"
RUN sed -i "s/session.cookie_httponly =/session.cookie_httponly = 1/g" "$PHP_INI_DIR/php.ini"

RUN apt-get update && apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev libbz2-dev
RUN docker-php-ext-install bz2
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && docker-php-ext-install gd
RUN docker-php-ext-configure pdo_mysql --with-pdo-mysql=mysqlnd && docker-php-ext-install pdo_mysql
RUN docker-php-ext-configure mysqli --with-mysqli=mysqlnd && docker-php-ext-install mysqli
