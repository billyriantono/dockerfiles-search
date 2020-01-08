FROM php:7.3.8-alpine
LABEL Maintainer="Asdrubal Gonzalez <agpenton@gmail.com"
RUN apk --update add wget curl git php php-curl php-openssl php-json php-phar php-dom bash sshpass git openssh-client rsync && rm /var/cache/apk/* && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer
CMD ["/bin/sh"]

ENTRYPOINT ["/bin/sh", "-c"]
