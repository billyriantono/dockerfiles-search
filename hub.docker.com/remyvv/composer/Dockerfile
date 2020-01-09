FROM alpine:3.2
MAINTAINER remyvv <remy@remysplace.de>

RUN apk add --update \
    ca-certificates \
    bash \
    git \
    mercurial \
    php-bz2 \
    php-cli \
    php-dom \
    php-gd \
    php-json \
    php-mcrypt \
    php-openssl \
    php-pdo \
    php-pear \
    php-phar \
    php-zip \
    php-ctype \
    subversion \
    unrar \
    && rm -rf /var/cache/apk/*

#php -r "readfile('https://getcomposer.org/installer');" > composer-setup.php
#php -r "if (hash_file('SHA384', 'composer-setup.php') === 'a52be7b8724e47499b039d53415953cc3d5b459b9d9c0308301f867921c19efc623b81dfef8fc2be194a5cf56945d223') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
#php composer-setup.php
#php -r "unlink('composer-setup.php');"

RUN php -r "readfile('https://getcomposer.org/installer');" > composer-setup.php \
    && php -r "if (hash_file('SHA384', 'composer-setup.php') === 'a52be7b8724e47499b039d53415953cc3d5b459b9d9c0308301f867921c19efc623b81dfef8fc2be194a5cf56945d223') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
    && php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
    && php -r "unlink('composer-setup.php');"

# Set up the application directory
VOLUME ["/app"]
WORKDIR /app