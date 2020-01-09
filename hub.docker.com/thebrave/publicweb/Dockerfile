FROM thebrave/nginx
MAINTAINER Jean Berniolles <jean@berniolles.fr>

RUN apk add --no-cache php-json php-zlib php-xml php-pdo php-phar php-openssl \
    php-pgsql \
    php-gd php-iconv php-mcrypt \
    php-curl php-opcache php-ctype php-apcu \
    php-intl php-bcmath php-dom php-xmlreader \
    php-pcntl php-posix

ADD config /config
ADD supervisord.conf /etc/supervisor/conf.d/ttrss-update-daemon.conf
