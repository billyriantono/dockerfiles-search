FROM php:7.2-fpm-alpine
RUN apk update
RUN apk add git libmcrypt-dev libpq curl-dev icu-dev libvpx-dev jpeg-dev libpng-dev libxpm-dev zlib-dev freetype libxml2-dev expat bzip2-dev unixodbc-dev aspell-dev net-snmp-libs pcre  tidyhtml-dev nodejs
RUN docker-php-ext-install mbstring curl json intl gd xml zip bz2 opcache
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer 
RUN composer global require webdevstudios/wds-coding-standards
RUN ~/.composer/vendor/bin/phpcs --config-set installed_paths ~/.composer/vendor/wp-coding-standards/wpcs,~/.composer/vendor/webdevstudios/wds-coding-standards/WebDevStudios
RUN npm install -g eslint eslint-config-wordpress sass-lint
