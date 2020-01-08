FROM ubuntu:vivid

MAINTAINER Simone Grignola <sito@grignola.ch>

ENV DEBIAN_FRONTEND noninteractive
ENV MEMORY_LIMIT 512M
ENV TIMEZONE Europe/Paris

RUN apt-get update

RUN apt-get install -y wget php5-fpm php5-cli php5-curl php5-gd php5-json php5-sqlite \
		       php5-pgsql php-pear php5-apcu php5-intl php5-mcrypt php5-mysqlnd \
		       php5-imagick php5-intl php5-xmlrpc php5-ldap php5-redis

RUN sed -i '/daemonize /c daemonize = no' /etc/php5/fpm/php-fpm.conf
RUN sed -i '/^ request_terminate_timeout /c request_terminate_timeout = 9000s' /etc/php5/fpm/pool.d/www.conf
RUN sed -i '/^listen /c listen = 0.0.0.0:9000' /etc/php5/fpm/pool.d/www.conf
RUN sed -i 's/^listen.allowed_clients/;listen.allowed_clients/' /etc/php5/fpm/pool.d/www.conf

RUN rm -rf /etc/php5/cli/php.ini && \
    ln -s /etc/php5/fpm/php.ini /etc/php5/cli/php.ini

RUN echo "date.timezone= ${TIMEZONE}" >>  /etc/php5/fpm/php.ini
RUN echo "phar.readonly = Off" >> /etc/php5/fpm/php.ini
RUN echo "default_charset = UTF-8" >> /etc/php5/fpm/php.ini

RUN sed -i -e "s/^max_execution_time\s*=.*/max_execution_time = 9000/" \
-e "s/^post_max_size\s*=.*/post_max_size = 3G/" \
-e "s/^short_open_tag\s*=.*/short_open_tag = On/" \
-e "s/^upload_max_filesize\s*=.*/upload_max_filesize = 3G\nupload_max_size = 3G/" \
-e "s/^memory_limit\s*=.*/memory_limit = ${MEMORY_LIMIT}/" /etc/php5/fpm/php.ini

RUN cd /tmp && \
    php -r "readfile('https://getcomposer.org/installer');" | php && \
    mv composer.phar /usr/local/bin/composer

VOLUME /var/www

CMD ["php5-fpm"]

EXPOSE 9000

RUN apt-get autoremove && \
    apt-get autoclean && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

