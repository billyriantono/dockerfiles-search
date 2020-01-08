FROM php:7.2-fpm
# Node should probably be handled in an separate container but in some of our current projects we are using Gulp 
# as a Task runner which also executes PHP Commands - thus these need to be in the same container. 
RUN export buildDeps='gcc libc6-dev make libfreetype6-dev  libjpeg62-turbo-dev libmcrypt-dev libpng-dev libjpeg62-turbo-dev libjpeg-dev libmcrypt-dev libpng-dev icu-devtools libicu-dev libbz2-dev' && \
    apt-get update && \
    apt-get install -y $buildDeps \
        icu-doc libicu57 libmcrypt-dev \
        gnupg \
        bzip2 \
        procps \
        git \
        unzip  \
        wget \
        vim \
        apt-transport-https \
        mysql-client \
        libmagickwand-dev \
        gnupg2 \
        sudo \
        netcat && \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-install -j$(nproc) gd && \
    docker-php-ext-configure bz2 --with-bz2 && \
    docker-php-ext-install -j$(nproc) bz2 && \
    docker-php-ext-configure mysqli --with-mysqli=mysqlnd && \
    docker-php-ext-install -j$(nproc) mysqli && \
    docker-php-ext-install -j$(nproc) iconv intl zip exif pdo_mysql && \
    pecl install imagick-3.4.3 && \
    docker-php-ext-enable imagick && \
    pecl install mcrypt-1.0.1 && \
    pecl install xdebug && \
    docker-php-ext-enable mcrypt && \
    docker-php-ext-install opcache && \
    docker-php-ext-enable opcache && \
    sed -i 's/%sudo\s\+ALL=(ALL:ALL)\sALL/%sudo ALL=NOPASSWD: ALL/' /etc/sudoers && \
    usermod -a -G sudo www-data && \
    usermod -s /bin/bash www-data && \
    chown www-data:www-data /var/www && \
    sudo -u www-data touch /var/www/.bashrc && \
    curl -sL https://deb.nodesource.com/setup_8.x | bash - && \
    apt install -y nodejs && \
    npm install -g yarn && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer 
    
RUN echo "if [ -f ~/.aliases ];\nthen . ~/.aliases\nfi" >> /var/www/.bashrc
COPY .aliases /var/www/.aliases
RUN chown www-data:www-data /var/www/.aliases

RUN  mkdir /php && chown -R www-data:www-data /php
    
COPY www.conf /usr/local/etc/php-fpm.d/www.conf
COPY php.ini /usr/local/etc/php/php.ini
COPY php-cli.ini /usr/local/etc/php/php-cli.ini
COPY docker-php-ext-xdebug.ini /usr/local/etc/php/conf-available/docker-php-ext-xdebug.ini
COPY docker-php-ext-xdebug-linux.ini /usr/local/etc/php/conf-available/docker-php-ext-xdebug-linux.ini
COPY xdebug-enable /usr/local/bin/xdebug-enable
COPY xdebug-enable-for-linux /usr/local/bin/xdebug-enable-for-linux
COPY xdebug-disable /usr/local/bin/xdebug-disable
COPY restart-php-fpm /usr/local/bin/restart-php-fpm
COPY startup.sh /startup.sh

CMD ["/bin/bash","/startup.sh"]
WORKDIR /php
USER www-data
