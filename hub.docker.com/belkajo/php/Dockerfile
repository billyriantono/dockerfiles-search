FROM belkajo/base
LABEL version="2.0"
LABEL name=belkajo/php

RUN dnf --setopt=install_weak_deps=False --best -y install  \
    gd \
    sendmail \
    ImageMagick && \
 dnf  --setopt=install_weak_deps=False --best -y install  \
    php56 \
    php56-php \
    php56-php-bcmath \
    php56-php-fpm  \
    php56-php-gd \
    php56-php-intl \
    php56-php-json \
    php56-php-mbstring \
    php56-php-mcrypt \
    php56-php-mysqlnd \
    php56-php-pear \
    php56-php-pecl-imagick \
    php56-php-pecl-xdebug \
    php56-php-pecl-zip \
    php56-php-soap \
    php56-php-xml \
    php56-php-opcache \
    php56-php-gmp\ 
    php56-php-pecl-libsodium && \
 dnf --setopt=install_weak_deps=False --best -y install  \
    php70 \
    php70-php \
    php70-php-bcmath \
    php70-php-fpm \
    php70-php-gd \
    php70-php-intl \
    php70-php-json \
    php70-php-mcrypt \
    php70-php-mbstring \
    php70-php-mysqlnd \
    php70-php-pear \
    php70-php-pecl-imagick \
    php70-php-pecl-xdebug \
    php70-php-pecl-zip \
    php70-php-soap \
    php70-php-gmp \
    php70-php-xml \
    php70-php-opcache \
    php70-php-pecl-libsodium && \
 dnf --setopt=install_weak_deps=False --best -y install \
    php71 \
    php71-php \
    php71-php-bcmath \
    php71-php-fpm \
    php71-php-gd \
    php71-php-intl \
    php71-php-json \
    php71-php-mbstring \
    php71-php-mcrypt \
    php71-php-mysqlnd \
    php71-php-pear \
    php71-php-pecl-imagick \
    php71-php-pecl-xdebug \
    php71-php-pecl-zip \
    php71-php-soap \
    php71-php-xml \
    php71-php-gmp \
    php71-php-opcache \
    php71-php-pecl-libsodium && \
 dnf --setopt=install_weak_deps=False --best -y install  \
    php72 \
    php72-php-common \
    php72-php-bcmath \
    php72-php-fpm \
    php72-php-gd \
    php72-php-intl \
    php72-php-json \
    php72-php-mbstring \
    php72-php-mysqlnd \
    php72-php-pear \
    php72-php-pecl-imagick \
    php72-php-pecl-xdebug \
    php72-php-pecl-zip \
    php72-php-soap \
    php72-php-xml \
    php72-php-opcache \
    php72-php-pecl-libsodium \
    php72-php-gmp \
    php72-php-sodium && \
 dnf --setopt=install_weak_deps=False --best -y install  \
    php73 \
    php73-php-common \
    php73-php-bcmath \
    php73-php-fpm \
    php73-php-gd \
    php73-php-intl \
    php73-php-json \
    php73-php-mbstring \
    php73-php-mysqlnd \
    php73-php-pear \
    php73-php-pecl-imagick \
    php73-php-pecl-xdebug \
    php73-php-pecl-zip \
    php73-php-soap \
    php73-php-xml \
    php73-php-opcache \
    php73-php-gmp \
    php73-php-sodium && \
 dnf --setopt=install_weak_deps=False --best -y install  \
    php74 \
    php74-php-common \
    php74-php-bcmath \
    php74-php-fpm \
    php74-php-gd \
    php74-php-intl \
    php74-php-json \
    php74-php-mbstring \
    php74-php-mcrypt \
    php74-php-mysqlnd \
    php74-php-pear \
    php74-php-pecl-imagick \
    php74-php-pecl-xdebug \
    php74-php-pecl-zip \
    php74-php-soap \
    php74-php-xml \
    php74-php-opcache \
    php74-php-gmp \
    php74-php-sodium && \
dnf clean all && \
alternatives --install /usr/bin/php php /usr/bin/php56 1000 && \
alternatives --install /usr/bin/php php /usr/bin/php70 1000 && \
alternatives --install /usr/bin/php php /usr/bin/php71 1000 && \
alternatives --install /usr/bin/php php /usr/bin/php72 1000 && \
alternatives --install /usr/bin/php php /usr/bin/php73 1000 && \
alternatives --install /usr/bin/php php /usr/bin/php74 1000 

ENV PHP=72
COPY config/beforeStart.sh /usr/local/bin/beforeStart.sh
COPY config/mhsendmail_linux_amd64.dms /usr/local/bin/mhsendmail
COPY config/composer.phar.default  /usr/local/bin/composer
RUN chmod +x /usr/local/bin/composer
RUN chmod +x /usr/local/bin/mhsendmail

EXPOSE 9000

CMD ["/usr/local/bin/php-fpm", "-F", "-R"]