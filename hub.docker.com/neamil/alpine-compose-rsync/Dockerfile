FROM alpine
RUN apk --update add rsync openssh sshpass wget curl git php php-curl php-iconv php-openssl php-json php-phar php-dom && rm /var/cache/apk/*
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer
