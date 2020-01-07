FROM alpine:3.9

LABEL Diogo Dias <saidogoid2@gmail.com>

ENV \
    DEPS="php7 php7-phar php7-bcmath php7-calendar php7-mbstring php7-exif php7-ftp php7-openssl php7-zip php7-sysvsem \
    	php7-sysvshm php7-sysvmsg php7-shmop php7-sockets php7-zlib php7-bz2 php7-curl php7-simplexml php7-xml php7-opcache \
    	php7-dom php7-xmlreader php7-xmlwriter php7-tokenizer php7-ctype php7-session php7-fileinfo php7-iconv php7-json php7-posix \
    	php7-gd curl ca-certificates runit vim php7-pdo_mysql php7-pdo \
        composer nodejs nodejs-npm git mysql-client"
        # \openrc"

RUN set -x \
    && apk update && apk upgrade \
    && apk add --no-cache $DEPS \
    && npm install -g gulp
    #&& docker-php-ext-install $DEPS

#ADD NEW httpd.conf with rewrite enable
ADD ./httpd.conf /etc/apache2/httpd.conf

WORKDIR /var/www

EXPOSE 80 443

#CMD ["/bin/sh"]

CMD ["/sbin/init"]

