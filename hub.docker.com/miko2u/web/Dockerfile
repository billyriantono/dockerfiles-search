FROM miko2u/centos6
MAINTAINER miko@cafelounge.net

# packages
RUN cd /tmp \
 && yum -y update \
 && yum -y install http://nginx.org/packages/centos/6/noarch/RPMS/nginx-release-centos-6-0.el6.ngx.noarch.rpm \
 && yum -y install nginx redis logrotate \
 && yum -y --enablerepo=remi,remi-php56 install \
	php-fpm php-cli php-common php-opcache php-mbstring \
	php-bcmath php-gd php-mcrypt php-pdo php-mysqlnd \
	php-process php-pecl-imagick php-xml \
 && yum -y --enablerepo=remi,remi-php56 clean all \
 && rm -rf /tmp/* /var/tmp/* /var/lib/yum/* /var/cache/yum/* \
 && sed -i.dist \
	-e 's/^expose_php =.*$/expose_php = Off/g' \
	-e 's,^;date.timezone =.*$,date.timezone = "Asia/Tokyo",g' \
	/etc/php.ini \
 && sed -i.dist \
	-e 's/^listen = 127.0.0.1:9000/listen = 9000/g' \
	-e 's/^listen.allowed_clients/;listen.allowed_clients/g' \
	-e 's,^;ping.path = .*$,ping.path = /ping,g' \
        -e 's/^;request_slowlog_timeout = .*$/request_slowlog_timeout = 1m/g' \
        -e 's/^;request_terminate_timeout = .*$/request_terminate_timeout = 30m/g' \
	/etc/php-fpm.d/www.conf \
 && find / -xdev -group redis -exec chgrp 496 {} \; && groupmod -g 496 redis \
 && find / -xdev -user redis -exec chown 496 {} \;  && usermod -u 496 redis \
 && find / -xdev -group nginx -exec chgrp 498 {} \; && groupmod -g 498 nginx \
 && find / -xdev -user nginx -exec chown 498 {} \;  && usermod -u 498 nginx \
 && cp -pr /etc/nginx/nginx.conf{,.dist} \
 && chkconfig messagebus off \
 && chkconfig nginx on \
 && chkconfig redis off \

# startup
COPY prepare /boot/
