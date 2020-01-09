FROM alpine

RUN apk update && apk upgrade

RUN apk add vim nano

RUN apk add bash curl unzip git
RUN apk add php-fpm php-bcmath php-dom php-gettext php-opcache php-session php-sockets php-tokenizer php-mysqlnd php-xmlrpc php-calendar php-fileinfo php-iconv php-openssl php-shmop php-sysvmsg php-xml php-phar php-xsl php-ctype php-ftp php-json php-pdo php-simplexml php-sysvsem php-xmlwriter php-wddx php-mysqli php-curl php-gd php-mbstring php-posix php-soap php-sysvshm php-exif php-xmlreader php-pdo_mysql

RUN /usr/bin/curl -sS https://getcomposer.org/installer | /usr/bin/php -- --install-dir=/usr/local/bin
RUN ln -s /usr/local/bin/composer.phar /usr/local/bin/composer

RUN wget https://phar.phpunit.de/phpunit-8.5.phar
RUN chmod +x phpunit-8.5.phar
RUN mv phpunit-8.5.phar /usr/local/bin
RUN ln -s /usr/local/bin/phpunit-8.5.phar /usr/local/bin/phpunit

RUN apk add nodejs npm

RUN apk add nginx

RUN mkdir /run/nginx

COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
COPY ./nginx/nginx.conf /etc/nginx/nginx.conf

RUN adduser -D -G 'www-data' www-data
RUN chown -R www-data:www-data /var/www

EXPOSE 80

STOPSIGNAL SIGTERM

WORKDIR /var/www

CMD /usr/sbin/php-fpm7 -D; nginx

RUN ln -sf /dev/stdout /var/log/nginx/access.log \
	&& ln -sf /dev/stdout /var/log/nginx/error.log \
	&& ln -sf /dev/stdout /var/log/php7/error.log