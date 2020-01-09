FROM php:alpine
LABEL maintainer="hitalos <hitalos@gmail.com>"

RUN apk update && apk upgrade && apk add bash git

# Install PHP extensions
ADD install-php.sh /usr/sbin/install-php.sh
RUN /usr/sbin/install-php.sh

WORKDIR /var/www
EXPOSE 80
