FROM alpine:latest

RUN apk add --no-cache php7-apache2 php7-openssl php7-json git && \
    rm -rf /var/www/localhost/htdocs/* /var/cache/apk/* && \
    adduser -u 82 -D -S -G www-data www-data && \
    mkdir -p /run/apache2 && \
    chown -R www-data:www-data /run/apache2 && \
    sed -i 's/max_execution_time = [0-9]\+/max_execution_time = 90/' /etc/php7/php.ini && \
    sed -i 's/max_input_time = [0-9]\+/max_input_time = 90/' /etc/php7/php.ini && \
    sed -i 's/memory_limit = [0-9]\+M/memory_limit = 128M/' /etc/php7/php.ini && \
    sed -i 's/post_max_size = [0-9]\+M/post_max_size = 50M/' /etc/php7/php.ini && \
    sed -i 's/upload_max_filesize = [0-9]\+M/upload_max_filesize = 50M/' /etc/php7/php.ini && \
    sed -i 's/ErrorLog logs\/error.log/ErrorLog \/dev\/stdout/' /etc/apache2/httpd.conf && \
    sed -i 's/CustomLog/#CustomLog/' /etc/apache2/httpd.conf && \
    sed -i 's/Listen 80/Listen 8080/' /etc/apache2/httpd.conf && \
    cd /tmp && git clone --branch docker https://github.com/librespeed/speedtest.git && \
    cd /tmp/speedtest && cp -R * /var/www/localhost/htdocs/ && \
    mv /var/www/localhost/htdocs/docker/standalone.php /var/www/localhost/htdocs/index.php && \
    chown -hR www-data:www-data /var/www/ && \
    apk del git && rm -rf /var/cache/apk/* /tmp/* /tmp/.[!.]*

USER www-data

EXPOSE 8080

CMD ["/usr/sbin/httpd", "-k", "start", "-D", "FOREGROUND", "-c", "ServerName localhost"]