FROM alpine:3.4
MAINTAINER "keoni84 - https://bitbucket.org/keoni84"

# Timezone
ENV TIMEZONE            UTC
ENV PHP_MEMORY_LIMIT    512M
ENV MAX_UPLOAD          50M
ENV PHP_MAX_FILE_UPLOAD 200
ENV PHP_MAX_POST        100M

# install mysql, apache and php and php extensions, tzdata, wget
RUN addgroup -g 1020 mysql && addgroup -g 1021 apache && \
adduser -u 1020 -G mysql -s /sbin/nologin -h /var/lib/mysql -D mysql && \
adduser -u 1021 -G apache -s /sbin/nologin -h /www -D apache && \
adduser -u 1026 -G apache -s /sbin/nologin -h /www -D webhost && \
echo "@community http://dl-cdn.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories && \
apk update && \
apk add \
mysql mysql-client \
apache2 \
curl wget \
tzdata \
php5-apache2 \
php5-cli \
php5-phar \
php5-zlib \
php5-zip \
php5-bz2 \
php5-ctype \
php5-mysqli \
php5-mysql \
php5-pdo_mysql \
php5-opcache \
php5-pdo \
php5-json \
php5-curl \
php5-gd \
php5-gmp \
php5-mcrypt \
php5-openssl \
php5-dom \
php5-xml \
php5-iconv \
supervisor

# configure timezone, mysql, apache
RUN cp /usr/share/zoneinfo/${TIMEZONE} /etc/localtime && \
echo "${TIMEZONE}" > /etc/timezone && \
mkdir -p /run/mysqld && \
chown -R mysql:mysql /run/mysqld /var/lib/mysql && \
mysql_install_db --user=mysql --verbose=1 --basedir=/usr --datadir=/var/lib/mysql --rpm > /dev/null && \
sed -i '/skip-external-locking/a log_error = \/var\/lib\/mysql\/error.log' /etc/mysql/my.cnf && \
sed -i '/skip-external-locking/a general_log = ON' /etc/mysql/my.cnf && \
sed -i '/skip-external-locking/a general_log_file = \/var\/lib\/mysql\/query.log' /etc/mysql/my.cnf && \
ln -s /usr/lib/libxml2.so.2 /usr/lib/libxml2.so && \
sed -i 's#AllowOverride None#AllowOverride All#' /etc/apache2/httpd.conf && \
sed -i 's#ServerName www.example.com:80#\nServerName localhost:80#' /etc/apache2/httpd.conf && \
sed -i 's#^DocumentRoot ".*#DocumentRoot "/www"#g' /etc/apache2/httpd.conf && \
sed -i 's#/var/www/localhost/htdocs#/www#g' /etc/apache2/httpd.conf && \
sed -i "s|;*date.timezone =.*|date.timezone = ${TIMEZONE}|i" /etc/php5/php.ini && \
sed -i "s|;*memory_limit =.*|memory_limit = ${PHP_MEMORY_LIMIT}|i" /etc/php5/php.ini && \
sed -i "s|;*upload_max_filesize =.*|upload_max_filesize = ${MAX_UPLOAD}|i" /etc/php5/php.ini && \
sed -i "s|;*max_file_uploads =.*|max_file_uploads = ${PHP_MAX_FILE_UPLOAD}|i" /etc/php5/php.ini && \
sed -i "s|;*post_max_size =.*|post_max_size = ${PHP_MAX_POST}|i" /etc/php5/php.ini && \
sed -i "s|;*cgi.fix_pathinfo=.*|cgi.fix_pathinfo= 0|i" /etc/php5/php.ini && \
sed -i 's/Listen 80/Listen 0.0.0.0:80/' /etc/apache2/httpd.conf && \
sed -i 's/User apache/User webhost/' /etc/apache2/httpd.conf && \
mkdir -p /run/apache2 && \
chown -R apache:apache /run/apache2 && \
echo "<?php phpinfo(); ?>" > /www/index.php && \
mysql_install_db --user=mysql --datadir=/var/lib/mysql && \
wget --no-check-certificate -O /tmp/php5-xdebug-2.5.5-r0.apk https://bitbucket.org/keoni84/alpine-lamp/downloads/php5-xdebug-2.5.5-r0.apk && \
apk add --no-cache --allow-untrusted /tmp/php5-xdebug-2.5.5-r0.apk && \
chmod 755 /www && \
chown -R apache:apache /www && \
rm -f /tmp/php5-xdebug-2.5.5-r0.apk

#Copy Files
COPY supervisord.conf /etc/supervisord.conf
COPY index.html /www/index.html
COPY phpinfo.php /www/phpinfo.php
COPY my.cnf /etc/mysql/my.cnf

# Configure xdebug and change ownership
RUN echo "zend_extension=xdebug.so" > /etc/php5/conf.d/xdebug.ini && \
echo -e "\n[XDEBUG]"  >> /etc/php5/conf.d/xdebug.ini && \
echo "xdebug.remote_enable=1" >> /etc/php5/conf.d/xdebug.ini && \
echo "xdebug.remote_connect_back=1" >> /etc/php5/conf.d/xdebug.ini && \
echo "xdebug.idekey=PHPSTORM" >> /etc/php5/conf.d/xdebug.ini && \
echo "xdebug.remote_log=\"/tmp/xdebug.log\"" >> /etc/php5/conf.d/xdebug.ini && \
sed -i 's/mysqli.default_socket =/mysqli.default_socket = "\/run\/mysqld\/mysqld.sock"/' /etc/php5/php.ini && \
sed -i 's/mysql.default_socket =/mysql.default_socket = "\/run\/mysqld\/mysqld.sock"/' /etc/php5/php.ini && \
chown mysql:root /etc/mysql/my.cnf

EXPOSE 80
#EXPOSE 3306

VOLUME ["/www","/var/lib/mysql","/var/log/apache2"]
CMD ["/usr/bin/supervisord", "-c", "/etc/supervisord.conf"]