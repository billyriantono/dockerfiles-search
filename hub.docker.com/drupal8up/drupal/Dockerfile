FROM ubuntu:16.04

MAINTAINER Ivan Berezhnov <ivan.berezhnov@icloud.com>

# Set the locale
RUN apt-get update \
    && apt-get install locales \
    && locale-gen en_US.UTF-8 \
    && apt-get update \
    && apt-get install -y python-software-properties software-properties-common \
    && LC_ALL=C.UTF-8 add-apt-repository -y ppa:ondrej/php \
    && apt-get update \
    && apt-get install -y nginx curl zip unzip git supervisor sqlite3 \
       php7.0-fpm php7.0-cli php7.0-common php7.0-mcrypt php7.0-gd php7.0-mysql php7.0-imap \
       php-memcached php7.0-mbstring php7.0-xml php7.0-curl php7.0-sqlite3 php7.0-xdebug \
       php7.0-ctype php7.0-json php7.0-opcache php7.0-phar php7.0-pgsql php-pear php7.0-pdo \
    && php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer \
    && mkdir /run/php \
    && apt-get remove --purge software-properties-common -y \
    && apt-get --purge autoremove -y \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && echo "daemon off;" >> /etc/nginx/nginx.conf \
    && ln -sf /dev/stdout /var/log/nginx/access.log \
    && ln -sf /dev/stderr /var/log/nginx/error.log

COPY default /etc/nginx/sites-available/default
COPY php-fpm.conf /etc/php/7.0/fpm/php-fpm.conf
COPY xdebug.ini /etc/php/7.0/mods-available/xdebug.ini
COPY opcache.ini /etc/php/7.0/mods-available/opcache.ini

EXPOSE 80 433

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY start-container /usr/local/bin/start-container
RUN  chmod +x usr/local/bin/start-container

CMD ["start-container"]