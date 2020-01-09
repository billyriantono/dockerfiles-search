FROM miko2u/centos6
MAINTAINER miko@cafelounge.net

RUN cd /tmp \
 && printf '[nginx-mainline]\n\
name=nginx repo\n\
baseurl=http://nginx.org/packages/mainline/centos/$releasever/$basearch/\n\
gpgcheck=0\n\
enabled=1\n\
' > /etc/yum.repos.d/nginx-main-line.repo \
 && yum -y --enablerepo=remi,remi-php70 install \
    php-fpm php-cli php-common php-opcache php-mbstring \
    php-bcmath php-gd php-mcrypt php-pdo php-mysqlnd \
    php-process php-pecl-imagick php-xml fuse-libs nginx ssmtp sudo git logrotate \
 && yum -y --enablerepo=remi,remi-php70 clean all \
 && rm -rf /var/tmp/* /var/lib/yum/* /var/cache/yum/* \
 && curl -sS https://getcomposer.org/installer | php \
 && mv composer.phar /usr/bin/composer \
 && sed -e "s/^mailhub=.*$/mailhub=172.17.0.1/g" \
        -i.dist /etc/ssmtp/ssmtp.conf \
 && sed -e 's/^listen = 127.0.0.1:9000/listen = 9000/g' \
        -e 's/^listen.allowed_clients/#listen.allowed_clients/g' \
        -e 's/^s;request_slowlog_timeout.*$/request_slowlog_timeout = 10/g' \
        -e 's/^s;request_terminate_timeout.*$/request_terminate_timeout = 90/g' \
        -i.dist /etc/php-fpm.d/www.conf \
 && sed -e 's,^;date.timezone =.*$,date.timezone = Asia/Tokyo,g' \
        -e 's/^expose_php =.*$/expose_php = Off/g' \
        -e 's/^post_max_size =.*$/post_max_size = 100M/g' \
        -e 's/^upload_max_filesize =.*$/upload_max_filesize = 100M/g' \
        -i.dist /etc/php.ini \
 && find / -xdev -group nginx -exec chgrp 498 {} \; && groupmod -g 498 nginx \
 && find / -xdev -user nginx -exec chown 498 {} \; && usermod -u 498 nginx \
 && cp -pr /etc/nginx/nginx.conf /etc/nginx/nginx.conf.dist \
 && chkconfig messagebus off \
 && chkconfig php-fpm on \
 && chkconfig nginx on

# init
COPY prepare /boot/

# expose
EXPOSE 80 443
