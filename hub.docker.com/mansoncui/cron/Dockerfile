FROM alpine:edge
MAINTAINER Cuibobo <cuibobo@kuaidihelp.com>

ENV LANG=C.UTF-8
ENV PHP_FPM_USER="www" 
ENV PHP_FPM_GROUP="www" 
ENV PHP_FPM_LISTEN_MODE="0660"
ENV PHP_MEMORY_LIMIT="512M"
ENV PHP_MAX_UPLOAD="50M"
ENV PHP_MAX_FILE_UPLOAD="200"
ENV PHP_MAX_POST="100M"
ENV PHP_DISPLAY_ERRORS="On"
ENV PHP_DISPLAY_STARTUP_ERRORS="On"
ENV PHP_ERROR_REPORTING="E_COMPILE_ERROR\|E_RECOVERABLE_ERROR\|E_ERROR\|E_CORE_ERROR"
ENV PHP_CGI_FIX_PATHINFO=0
ENV TIMEZONE="Asia/Shanghai"

COPY ./service.sh /root/
COPY ./ErrorLogWriterOnlineTest.phar /root/
COPY ./rsyslog.conf /opt/

RUN  apk update && \
     apk add --no-cache tzdata  && \
	apk add --no-cache php7-fpm \
		       php7 \
                       php7-mcrypt \
                       php7-soap  \
                       php7-openssl \
                       php7-gmp \
                       php7-pdo_odbc \
                       php7-json \
                       php7-dom \
                       php7-pdo \
                       php7-zip \
		       php7-mysqli \
		       php7-phar \
                       php7-sqlite3 \
                       php7-apcu \
		       php7-pdo_pgsql \
                       php7-bcmath \
                       php7-gd \
                       php7-odbc \
                       php7-pdo_mysql \
                       php7-pdo_sqlite \
                       php7-gettext \
                       php7-xmlreader \
                       php7-xmlrpc \
                       php7-bz2 \
                       php7-sockets \
                       php7-xmlwriter \
		       php7-xsl \
		       php7-tokenizer \
		       php7-ftp \
		       php7-posix \
                       php7-fileinfo \
		       php7-shmop \
		       php7-mbstring \
                       php7-iconv \
                       php7-pdo_dblib \
                       php7-curl \
		       php7-session \
                       php7-ctype \
		       php7-simplexml \
                       php7-redis && \
		sed -i "s|;listen.owner\s*=\s*nobody|listen.owner = ${PHP_FPM_USER}|g" /etc/php7/php-fpm.d/www.conf && \
sed -i -e "s/;daemonize\s*=\s*yes/daemonize = no/g" /etc/php7/php-fpm.conf && \
sed -i -e "s/;slowlog/slowlog/g" /etc/php7/php-fpm.d/www.conf && \
sed -i "s|;listen.group\s*=\s*nobody|listen.group = ${PHP_FPM_GROUP}|g" /etc/php7/php-fpm.conf && \
sed -i "s|;listen.mode\s*=\s*0660|listen.mode = ${PHP_FPM_LISTEN_MODE}|g" /etc/php7/php-fpm.conf && \
sed -i "s|user\s*=\s*nobody|user = ${PHP_FPM_USER}|g" /etc/php7/php-fpm.conf && \
sed -i "s|group\s*=\s*nobody|group = ${PHP_FPM_GROUP}|g" /etc/php7/php-fpm.conf && \
sed -i "s|;log_level\s*=\s*notice|log_level = notice|g" /etc/php7/php-fpm.conf && \
sed -i "s|display_errors\s*=\s*Off|display_errors = ${PHP_DISPLAY_ERRORS}|i" /etc/php7/php.ini && \
sed -i "s|display_startup_errors\s*=\s*Off|display_startup_errors = ${PHP_DISPLAY_STARTUP_ERRORS}|i" /etc/php7/php.ini && \
sed -i "s|error_reporting\s*=\s*E_ALL & ~E_DEPRECATED & ~E_STRICT|error_reporting = ${PHP_ERROR_REPORTING}|i" /etc/php7/php.ini && \
sed -i "s|;*memory_limit =.*|memory_limit = ${PHP_MEMORY_LIMIT}|i" /etc/php7/php.ini && \
sed -i "s|;*upload_max_filesize =.*|upload_max_filesize = ${PHP_MAX_UPLOAD}|i" /etc/php7/php.ini && \
sed -i "s|;*max_file_uploads =.*|max_file_uploads = ${PHP_MAX_FILE_UPLOAD}|i" /etc/php7/php.ini && \
sed -i "s|;*post_max_size =.*|post_max_size = ${PHP_MAX_POST}|i" /etc/php7/php.ini && \
sed -i "s|;*cgi.fix_pathinfo=.*|cgi.fix_pathinfo= ${PHP_CGI_FIX_PATHINFO}|i" /etc/php7/php.ini && \
cp /usr/share/zoneinfo/${TIMEZONE} /etc/localtime && \
echo "${TIMEZONE}" > /etc/timezone && \
sed -i "s|;*date.timezone =.*|date.timezone = ${TIMEZONE}|i" /etc/php7/php.ini && \
        mkdir /www && \
        apk del tzdata curl && \
	adduser -D -g 'www' www && \
        chown -R www:www /www && \
	apk add rsyslog logrotate && \
	rm -f /etc/rsyslog.conf && \
	mv /opt/rsyslog.conf /etc/ && \
        apk add --no-cache --repository http://dl-4.alpinelinux.org/alpine/edge/testing gnu-libiconv && \
	rm -rf /var/cache/apk/*

ENV LD_PRELOAD /usr/lib/preloadable_libiconv.so php

WORKDIR /www
VOLUME ["/www"]

EXPOSE 80
CMD ["/root/service.sh"]
