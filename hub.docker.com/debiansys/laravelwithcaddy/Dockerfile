FROM phusion/baseimage:latest

RUN locale-gen en_US.UTF-8  
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN apt-get update && \
apt-get install -y software-properties-common && \
LC_ALL=en_US.UTF-8 add-apt-repository ppa:ondrej/php && \
apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6 && \
echo "deb [ arch=amd64,arm64 ] http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.4 multiverse" | tee /etc/apt/sources.list.d/mongodb-org-3.4.list && \
apt-get update && \
apt-get upgrade -y && \
BUILD_PACKAGES="python3 ffmpeg mediainfo git curl php7.1-fileinfo php7.1-xmlwriter htop dialog php7.1-tokenizer php7.1-imagick php7.1-opcache php7.1-xmlreader php7.1-gettext php7.1-soap php7.1-xmlrpc php7.1-phar php7.1-json php7.1-iconv php7.1-fpm php7.1-exif php7.1-zip php7.1-bz2 php7.1-mysql php-memcached php7.1-mysql php7.1-curl php7.1-gd php7.1-intl php7.1-dom php7.1-mcrypt php7.1-sqlite3 php7.1-tidy php7.1-pgsql php7.1-xml php7.1-mongodb php7.1-redis php7.1-xdebug nano php-mbstring mongodb-org-tools wget" && \
apt-get -y install $BUILD_PACKAGES && \
apt-get remove --purge -y software-properties-common && \
apt-get autoremove -y && \
apt-get clean && \
apt-get autoclean && \
echo -n > /var/lib/apt/extended_states && \
rm -rf /var/lib/apt/lists/* && \
rm -rf /usr/share/man/?? && \
rm -rf /usr/share/man/??_* && \
find /etc/php/7.1/cli/conf.d/ -name "*.ini" -exec sed -i -re 's/^(\s*)#(.*)/\1;\2/g' {} \; && \
rm /etc/php/7.1/cli/conf.d/20-mcrypt.ini && rm /etc/php/7.1/fpm/conf.d/20-mcrypt.ini && \
phpenmod mcrypt && mkdir /run/php && chmod 777 /run/php && \
sed -i -e "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/g" /etc/php/7.1/fpm/php.ini && \
sed -i -e "s/upload_max_filesize\s*=\s*2M/upload_max_filesize = 100M/g" /etc/php/7.1/fpm/php.ini && \
sed -i -e "s/post_max_size\s*=\s*8M/post_max_size = 100M/g" /etc/php/7.1/fpm/php.ini && \
sed -i -e "s/;daemonize\s*=\s*yes/daemonize = no/g" /etc/php/7.1/fpm/php-fpm.conf && \
mkdir -p /var/www && \
mkdir -p /etc/caddy/conf.d && \
usermod -u 1000 www-data && \
usermod -a -G users www-data && \
chown -R www-data:www-data /var/www/ && \
mkdir -p /etc/service/caddy && \
mkdir -p /etc/service/phpfpm && \
mkdir /etc/service/logs && \
mkdir -p /etc/my_init.d && \
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
php -r "if (hash_file('SHA384', 'composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" && \
php composer-setup.php --install-dir=/usr/local/bin --filename=composer && \
php -r "unlink('composer-setup.php');" && \
composer global require hirak/prestissimo
#wget -O /bin/caddy  https://caddyserver.com/download/linux/amd64?plugins=http.cache,http.cgi,http.cors,http.expires,http.filemanager,http.filter,http.forwardproxy,http.git,http.ipfilter,http.mailout,http.minify,http.ratelimit,http.realip,http.restic,http.upload&license=personal



COPY ./fpmpool.conf /etc/php/7.1/fpm/pool.d/www.conf
COPY ./caddy /bin/caddy
ADD logrotate_laravel.conf /etc/logrotate.d/laravel
COPY ./caddy.conf /caddy.conf

ADD ./caddy.sh /etc/service/caddy/run
ADD ./phpfpm.sh /etc/service/phpfpm/run
ADD ./boot.sh /etc/my_init.d/boot.sh
ADD ./logs.sh /etc/service/logs/run

RUN chmod +x /etc/service/caddy/run && chmod +x /etc/service/phpfpm/run && chmod +x /etc/my_init.d/boot.sh && chmod 777 /etc/service/logs/run

RUN rm /var/www/bootstrap/cache/config.php > /dev/null 2>&1 || true
RUN rm /var/www/.env > /dev/null 2>&1 || true


ENV APP_ENV=local \
    APP_DEBUG=true \
    DB_HOST=db \
    DB_DATABASE=laravel \
    APP_URL="http://laravel.dev" \
    APP_KEY="kD7qEXQBJUmURfVHvsHyWTVG9UmkZoUR" \
    DB_TYPE=mongodb \
    DB_PORT=27017 \
    QUEUE_DRIVER=beanstalkd \
    QUEUE_HOST=queue \
    CACHE_DRIVER=redis \
    REDIS_HOST=redis \
    REDIS_PORT=6379 \
    SESSION_DRIVER=redis \
    APP_FILESYSTEM=local  \
    MAIL_PRETEND=true


CMD ["/sbin/my_init"]
EXPOSE 80