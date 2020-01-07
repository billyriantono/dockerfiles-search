#
# PHP5 Dockerfile
#
# https://github.com/julienvincent/docker-nginx-php
#

FROM julienvincent/nginx
MAINTAINER Julien Vincent "julienlucvincent@gmail.com"

# Install PHP5

RUN usermod -a -G staff nginx

RUN apt-get update && \
    apt-get -y install php5 php5-fpm php5-curl php5-json php5-mcrypt php5-mssql php5-mysqlnd php5-pgsql php5-sqlite && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Add configs
COPY container/php-fpm.conf /etc/nginx/php-fpm.conf
COPY container/php.ini /etc/php5/fpm/php.ini
COPY container/www.conf /etc/php5/fpm/pool.d/www.conf
COPY container/default.conf /etc/nginx/conf.d/default.conf
COPY container/supervisord.conf /etc/supervisor/conf.d/supervisord.conf

COPY container/index.php /data/www/public/index.php

# Container Config
CMD ["/usr/bin/supervisord"]
EXPOSE 80 443