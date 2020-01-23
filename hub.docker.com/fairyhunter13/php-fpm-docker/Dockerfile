FROM php:7.2-fpm


ENV TIMEZONE            Asia/Jakarta
ENV PHP_MEMORY_LIMIT    512M
ENV MAX_UPLOAD          50M
ENV PHP_MAX_FILE_UPLOAD 200
ENV PHP_MAX_POST        100M

RUN apt-get update; \
    apt-get install vim --no-install-recommends -y; \
    sed -i "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/g" $PHP_INI_DIR/php.ini-production ; \
    sed -i "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/g" $PHP_INI_DIR/php.ini-development ; \
    sed -i "s|;*date.timezone =.*|date.timezone = ${TIMEZONE}|i" $PHP_INI_DIR/php.ini-development; \
    sed -i "s|;*date.timezone =.*|date.timezone = ${TIMEZONE}|i" $PHP_INI_DIR/php.ini-production; \
    sed -i "s|;*memory_limit =.*|memory_limit = ${PHP_MEMORY_LIMIT}|i" $PHP_INI_DIR/php.ini-development                              ; \
    sed -i "s|;*memory_limit =.*|memory_limit = ${PHP_MEMORY_LIMIT}|i" $PHP_INI_DIR/php.ini-production                              ; \
    sed -i "s|;*upload_max_filesize =.*|upload_max_filesize = ${MAX_UPLOAD}|i" $PHP_INI_DIR/php.ini-development                      ; \
    sed -i "s|;*upload_max_filesize =.*|upload_max_filesize = ${MAX_UPLOAD}|i" $PHP_INI_DIR/php.ini-production                       ; \
    sed -i "s|;*max_file_uploads =.*|max_file_uploads = ${PHP_MAX_FILE_UPLOAD}|i" $PHP_INI_DIR/php.ini-development                    ; \
    sed -i "s|;*max_file_uploads =.*|max_file_uploads = ${PHP_MAX_FILE_UPLOAD}|i" $PHP_INI_DIR/php.ini-production                    ; \
    # sed -i -e "s/post_max_size\s*=\s*8M/post_max_size = 100M/g" $PHP_INI_DIR/php.ini                                      ; \
    # sed -i -e "s/variables_order = \"GPCS\"/variables_order = \"EGPCS\"/g" $PHP_INI_DIR/php.ini                           ; \
    # sed -i -e "s/;daemonize\s*=\s*yes/daemonize = no/g" $PHP_INI_DIR/php-fpm.conf                                         ; \
    # sed -i -e "s/error_log = \/var\/log\/php-fpm.log;/error_log = \/proc\/self\/fd\/2;/g" $PHP_INI_DIR/php-fpm.conf       ; \
    # sed -i -e "s/;catch_workers_output\s*=\s*yes/catch_workers_output = yes/g" $PHP_INI_DIR/php-fpm.conf                  ; \
    # sed -i -e "s/pm.max_children = 5/pm.max_children = 24/g" $PHP_INI_DIR/php-fpm.conf                                     ; \
    # sed -i -e "s/pm.start_servers = 2/pm.start_servers = 5/g" $PHP_INI_DIR/php-fpm.conf                                   ; \
    # sed -i -e "s/pm.min_spare_servers = 1/pm.min_spare_servers = 5/g" $PHP_INI_DIR/php-fpm.conf                           ; \
    # sed -i -e "s/pm.max_spare_servers = 3/pm.max_spare_servers = 5/g" $PHP_INI_DIR/php-fpm.conf                           ; \
    # sed -i -e "s/;pm.max_requests = 500/pm.max_requests = 200/g" $PHP_INI_DIR/php-fpm.conf                                ; \
    # sed -i -e "s/user = nobody/user = www-data/g" $PHP_INI_DIR/php-fpm.conf                                                  ; \
    # sed -i -e "s/group = nobody/group = www-data/g" $PHP_INI_DIR/php-fpm.conf                                                ; \
    # sed -i -e "s/;listen.mode = 0660/listen.mode = 0666/g" $PHP_INI_DIR/php-fpm.conf                                      ; \
    # sed -i -e "s/;listen.owner = nobody/listen.owner = www-data/g" $PHP_INI_DIR/php-fpm.conf                                 ; \
    # sed -i -e "s/;listen.group = nobody/listen.group = www-data/g" $PHP_INI_DIR/php-fpm.conf                                 ; \
    # sed -i -e "s/;pm.status_path = \/status/pm.status_path = \/status/g" $PHP_INI_DIR/php-fpm.conf                           ; \
    # sed -i -e "s/;ping.path = \/ping/ping.path = \/ping/g" $PHP_INI_DIR/php-fpm.conf                                         ; \
    # sed -i -e "s/;ping.response = pong /ping.response = pong g/g" $PHP_INI_DIR/php-fpm.conf                                  ; \
    # sed -i -e "s/;opcache.enable_cli=.*/opcache.enable_cli=1/" $PHP_INI_DIR/php.ini                                        ; \
    # sed -i -e "s/;opcache.memory_consumption=.*/opcache.memory_consumption=512/" $PHP_INI_DIR/php.ini                      ; \
    # sed -i -e "s/;opcache.interned_strings_buffer=.*/opcache.interned_strings_buffer=8/" $PHP_INI_DIR/php.ini            ; \ 
    # sed -i -e "s/;opcache.max_accelerated_files=.*/opcache.max_accelerated_files=8192/" $PHP_INI_DIR/php.ini            ; \ 
    # sed -i -e "s/;opcache.revalidate_path=.*/opcache.revalidate_path=1/" $PHP_INI_DIR/php.ini                              ; \ 
    # sed -i -e "s/;opcache.fast_shutdown=.*/opcache.fast_shutdown=1/" $PHP_INI_DIR/php.ini                                  ; \ 
    # sed -i -e "s/;opcache.enable_file_override=.*/opcache.enable_file_override=1/" $PHP_INI_DIR/php.ini                    ; \ 
    # sed -i -e "s/;opcache.validate_timestamps=.*/;opcache.validate_timestamps=1/" $PHP_INI_DIR/php.ini                     ; \ 
    # sed -i -e "s/;opcache.revalidate_freq=.*/opcache.revalidate_freq=0/" $PHP_INI_DIR/php.ini                              ; 
    docker-php-ext-install pdo pdo_mysql mysqli; 

RUN usermod -u 1000 www-data;


WORKDIR /app

CMD ["php-fpm"]

