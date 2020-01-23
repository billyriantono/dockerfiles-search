FROM debian:jessie
RUN mkdir /logs ; mkdir /www ; mkdir /www/web && \
    apt-get update && \
    apt-get install -y curl vim && \
    apt-get install -y nginx supervisor && \
    sed -i 's/\/var\/log\/nginx\/access.log/\/logs\/nginx_access.log/g' /etc/nginx/nginx.conf && \
    sed -i 's/\/var\/log\/nginx\/error.log/\/logs\/nginx_error.log/g' /etc/nginx/nginx.conf && \

    curl -o /tmp/dotdeb.gpg https://www.dotdeb.org/dotdeb.gpg && \
    apt-key add /tmp/dotdeb.gpg && \
    rm -f /tmp/dotdeb.gpg && \
    echo 'deb http://packages.dotdeb.org jessie all' >> /etc/apt/sources.list && \
    echo 'deb-src http://packages.dotdeb.org jessie all' >> /etc/apt/sources.list && \
    
    apt-get update && \
    apt-get install -y php7.0-mysql php7.0-fpm php7.0-curl php7.0-mcrypt php7.0-gd php7.0-redis && \
    chown www-data:www-data /logs  && \

    sed -i 's/\/var\/log\/php7.0-fpm.log/\/logs\/fpm.log/g' /etc/php/7.0/fpm/php-fpm.conf && \
    sed -i 's/upload_max_filesize/#upload_max_filesize/g' /etc/php/7.0/cli/php.ini && \
    sed -i 's/upload_max_filesize/#upload_max_filesize/g' /etc/php/7.0/fpm/php.ini && \

    sed -i 's/error_reporting/#error_reporting/g' /etc/php/7.0/fpm/php.ini && \
    sed -i 's/error_reporting/#error_reporting/g' /etc/php/7.0/cli/php.ini && \

    sed -i 's/display_errors/#display_errors/g' /etc/php/7.0/fpm/php.ini && \
    sed -i 's/display_errors/#display_errors/g' /etc/php/7.0/cli/php.ini && \

    sed -i 's/track_errors/#track_errors/g' /etc/php/7.0/fpm/php.ini && \
    sed -i 's/track_errors/#track_errors/g' /etc/php/7.0/cli/php.ini && \

    sed -i 's/display_startup_errors/#display_startup_errors/g' /etc/php/7.0/fpm/php.ini && \
    sed -i 's/display_startup_errors/#display_startup_errors/g' /etc/php/7.0/cli/php.ini && \

    apt-get install -y make php7.0-dev php-pear libyaml-dev && \
    pecl install yaml-2.0.0 && \
    echo "extension=yaml.so" > /etc/php/7.0/cli/conf.d/yaml.ini && \
    echo "extension=yaml.so" > /etc/php/7.0/fpm/conf.d/yaml.ini && \
    apt-get remove -y php7.0-dev && \
    apt-get autoremove -y && \

    rm -rf /var/lib/apt/lists/*

COPY supervisord.conf /etc/supervisor/supervisord.conf
COPY nginx /templates/nginx/
COPY php /templates/php/
COPY startup.sh /

COPY nginx/devlink.ca.crt /usr/local/share/ca-certificates/devlink.ca.crt
RUN update-ca-certificates


RUN chmod +x /startup.sh

EXPOSE 80 
EXPOSE 443

CMD ["sh","-c","/startup.sh"]
