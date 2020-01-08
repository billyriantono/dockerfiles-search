FROM alpine:3.5
MAINTAINER WPLib Team <team@wplib.org>

# Install PHP extensions and PECL modules.
RUN apk --update add --no-cache bash \
    curl \
    gnupg \
    imagemagick \
    openssl \
    php7 \
    php7-fpm \
    php7-bcmath \
    php7-curl \
    php7-ftp \
    php7-gd \
    php7-gettext \
    php7-intl \
    php7-iconv \
    php7-json \
    php7-mbstring \
    php7-mcrypt \
    php7-mysqli \
    php7-opcache \
    php7-openssl \
    php7-pcntl \
    php7-pspell \
    php7-session \
    php7-xdebug \
    php7-xml \
    php7-zip \
    && mkdir -p /run/php \
    && ln -sf /proc/self/fd/2 /var/log/php7.0-fpm.log \
    && wget https://github.com/mailhog/mhsendmail/releases/download/v0.2.0/mhsendmail_linux_amd64 \
    && mv mhsendmail_linux_amd64 /usr/local/bin/mhsendmail \
    && chmod +x /usr/local/bin/mhsendmail

COPY files /

EXPOSE 9000

CMD "php-fpm7"