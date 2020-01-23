FROM alpine:edge
MAINTAINER AlphaLayer - https://github.com/alphalayer

# Timezone
ENV TIMEZONE            Europe/Paris
ENV PHP_MEMORY_LIMIT    1024M
ENV MAX_UPLOAD          50M
ENV PHP_MAX_FILE_UPLOAD 200
ENV PHP_MAX_POST        100M
ENV DUMB_INIT_VERSION   1.2.2

RUN set -x \
	&& addgroup -g 82 -S www-data \
	&& adduser -u 82 -D -S -G www-data www-data
# 82 is the standard uid/gid for "www-data" in Alpine

ENV PHP_EXTRA_CONFIGURE_ARGS --enable-fpm --with-fpm-user=www-data --with-fpm-group=www-data

RUN echo "@edge-main http://dl-cdn.alpinelinux.org/alpine/edge/main" >> /etc/apk/repositories \
    && echo "@edge-community http://dl-cdn.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories \
    && echo "@edge-testing http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories \
	&& apk update && apk upgrade \
    && apk add -U shadow mailutils@edge-testing ssmtp openrc git nano unzip gzip mysql mysql-client curl wget vsftpd  \
    php7@edge-community \
    php7-dev@edge-community \
    php7-common@edge-community \
    php7-apache2@edge-community \
    php7-bcmath@edge-community \
    php7-xmlwriter@edge-community \
    php7-ctype@edge-community \
    php7-curl@edge-community \
    php7-exif@edge-community \
    php7-gd@edge-community \
    php7-iconv@edge-community \
    php7-intl@edge-community \
    php7-json@edge-community \
    php7-mbstring@edge-community \
    php7-openssl@edge-community \
    php7-pcntl@edge-community \
    php7-pdo@edge-community \
    php7-mysqlnd@edge-community \
    php7-pdo_mysql@edge-community \
    php7-pdo_pgsql@edge-community \
    php7-phar@edge-community \
    php7-posix@edge-community \
    php7-session@edge-community \
    php7-xml@edge-community \
    php7-simplexml@edge-community \
    php7-mcrypt@edge-community \
    php7-mysqli@edge-community \
    php7-xsl@edge-community \
    php7-zip@edge-community \
    php7-zlib@edge-community \
    php7-dom@edge-community \
    php7-fpm@edge-community \
    php7-tokenizer@edge-community \
    php7-xdebug@edge-community \
    && rm -rf /var/cache/apk/*

#RUN docker-php-ext-install mysqli pdo pdo_mysql
    
RUN curl -sS https://getcomposer.org/installer | \
    php -- --install-dir=/usr/bin --filename=composer

# ftp
RUN adduser -h /www -s /bin/false -D files

RUN echo "local_enable=YES" >> /etc/vsftpd/vsftpd.conf \
  && echo "chroot_local_user=YES" >> /etc/vsftpd/vsftpd.conf \
  && echo "write_enable=YES" >> /etc/vsftpd/vsftpd.conf \
  && echo "local_umask=022" >> /etc/vsftpd/vsftpd.conf \
  && echo "passwd_chroot_enable=yes" >> /etc/vsftpd/vsftpd.conf \
  && echo 'seccomp_sandbox=NO' >> /etc/vsftpd/vsftpd.conf \
  && echo 'pasv_enable=Yes' >> /etc/vsftpd/vsftpd.conf \
  && echo 'pasv_max_port=10100' >> /etc/vsftpd/vsftpd.conf \
  && echo 'pasv_min_port=10090' >> /etc/vsftpd/vsftpd.conf \
  && echo 'allow_writeable_chroot=YES' >> /etc/vsftpd/vsftpd.conf \  
  && sed -i "s/anonymous_enable=YES/anonymous_enable=NO/" /etc/vsftpd/vsftpd.conf

ADD configs/docker-entrypoint.sh /
	
# Apache
RUN apk update && apk upgrade \
	&& apk add apache2 libxml2-dev apache2-utils && \
	sed -i 's#^DocumentRoot ".*#DocumentRoot "/www"#g' /etc/apache2/httpd.conf && \
    sed -i 's#AllowOverride [Nn]one#AllowOverride All#' /etc/apache2/httpd.conf && \   
    sed -i 's/^#ServerName.*/ServerName localhost:80/' /etc/apache2/httpd.conf && \        
    sed -i 's/Options Indexes/Options /g' /etc/apache2/httpd.conf && \
	sed -i 's#/var/www/localhost/htdocs#/www#g' /etc/apache2/httpd.conf && \
	sed -i 's|#LoadModule rewrite_module modules/mod_rewrite.so|LoadModule rewrite_module modules/mod_rewrite.so|i' /etc/apache2/httpd.conf && \
	mkdir -p /run/apache2 && \
    chown -R apache:apache /run/apache2

# Mysql
RUN mkdir -p /run/mysqld && \
    chown -R mysql:mysql /run/mysqld /var/lib/mysql && \
    mysql_install_db --user=mysql --verbose=1 --basedir=/usr --datadir=/var/lib/mysql --rpm > /dev/null
	
# PHP Conf
RUN sed -i "s|;*date.timezone =.*|date.timezone = ${TIMEZONE}|i" /etc/php7/php.ini && \
    sed -i "s|;*memory_limit =.*|memory_limit = ${PHP_MEMORY_LIMIT}|i" /etc/php7/php.ini && \
    sed -i "s|;*upload_max_filesize =.*|upload_max_filesize = ${MAX_UPLOAD}|i" /etc/php7/php.ini && \
    sed -i "s|;*max_file_uploads =.*|max_file_uploads = ${PHP_MAX_FILE_UPLOAD}|i" /etc/php7/php.ini && \
    sed -i "s|;*post_max_size =.*|post_max_size = ${PHP_MAX_POST}|i" /etc/php7/php.ini && \
    sed -i "s|;*cgi.fix_pathinfo=.*|cgi.fix_pathinfo= 0|i" /etc/php7/php.ini && \    
	#mkdir /www && \
	chmod a-w /www && \
    echo "<?php phpinfo(); ?>" > /www/index.php && \
    chown -R www-data:www-data /www

# Configure xdebug
RUN echo "zend_extension=xdebug.so" > /etc/php7/conf.d/xdebug.ini && \ 
    echo -e "\n[XDEBUG]"  >> /etc/php7/conf.d/xdebug.ini && \ 
    echo "xdebug.remote_enable=1" >> /etc/php7/conf.d/xdebug.ini && \  
    echo "xdebug.remote_connect_back=1" >> /etc/php7/conf.d/xdebug.ini && \ 
    echo "xdebug.idekey=PHPSTORM" >> /etc/php7/conf.d/xdebug.ini && \ 
    echo "xdebug.remote_log=\"/tmp/xdebug.log\"" >> /etc/php7/conf.d/xdebug.ini
	
WORKDIR /www

EXPOSE 80 3306 443 20 21 10090-10100

#RUN usermod -u 1000 www-data
#RUN usermod -G 50 www-data

#VOLUME ["/www","/var/lib/mysql","/etc/mysql/"]

RUN chmod u+x /docker-entrypoint.sh

CMD /docker-entrypoint.sh	