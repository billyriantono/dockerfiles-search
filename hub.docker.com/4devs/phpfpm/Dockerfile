FROM 4devs/php:5.6

RUN yum -y install php-fpm && yum clean all

RUN useradd nginx -s /sbin/nologin && \
    chown nginx:nginx /var/www && \
    sed -i 's/user = apache/user = nginx/g' /etc/php-fpm.d/www.conf && \
    sed -i 's/group = apache/group = nginx/g' /etc/php-fpm.d/www.conf && \
    sed -i 's/listen = 127.0.0.1:9000/listen = 9000/g' /etc/php-fpm.d/www.conf && \
    sed -i 's/listen.allowed_clients = 127.0.0.1/#listen.allowed_clients =/g' /etc/php-fpm.d/www.conf && \
    sed -i 's/;pm.status_path/pm.status_path/g' /etc/php-fpm.d/www.conf && \
    sed -i 's/slowlog = \/var\/log\/php-fpm\/www-slow.log/slowlog = \/dev\/stdout/g' /etc/php-fpm.d/www.conf && \
    sed -i 's/error_log = \/var\/log\/php-fpm\/error.log/error_log = \/dev\/stdout/g' /etc/php-fpm.conf

EXPOSE 9000

CMD ["php-fpm", "-F"]
