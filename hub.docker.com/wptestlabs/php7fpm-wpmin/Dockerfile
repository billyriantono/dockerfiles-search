FROM alpine:latest
LABEL desc="Php7Fpm-WpMin" repo="github.com/WpTestLabs/Php7Fpm-WpMin" maintainer="WpTestLabs <___@gmail.com>"

RUN apk update && \
    apk add php7-fpm php7-json php7-zlib php7-xml php7-pdo php7-phar php7-openssl \
    php7-pdo_mysql php7-mysqli php7-session   php7-gd php7-iconv php7-mcrypt \
    php7-curl php7-opcache php7-ctype php7-apcu \
    php7-intl php7-bcmath php7-dom php7-mbstring php7-xmlreader mysql-client curl && apk add -u musl && \
    rm -rf /var/cache/apk/*

#   -F  -- Force to stay in Foreground ie no deamonize 
CMD ["/usr/sbin/php-fpm7", "-F"]
