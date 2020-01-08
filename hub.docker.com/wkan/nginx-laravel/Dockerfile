# wkan/laravel-dev

FROM debian:jessie
MAINTAINER Wkan wangkan1119@gmail.com

# Let the conatiner know that there is no tty
ENV DEBIAN_FRONTEND noninteractive

# install
RUN apt-get update && \
apt-get install -y git curl supervisor && \
curl -sS http://nginx.org/keys/nginx_signing.key | apt-key add - && \
echo 'deb http://nginx.org/packages/debian/ jessie nginx' >> /etc/apt/sources.list && \
echo 'deb-src http://nginx.org/packages/debian/ jessie nginx' >> /etc/apt/sources.list && \
apt-get update && \
apt-get upgrade -y && \
apt-get install -y \
nginx \
php5-fpm \
php-apc \
php5-curl \
php5-gd \
php5-intl \
php5-mcrypt \
php5-memcache \
php5-mysql \
php5-sqlite \
php5-pgsql \
php5-mongo \
php5-tidy \
php5-xmlrpc \
php5-xsl && \
curl -sS https://getcomposer.org/installer | php && \
mv composer.phar /usr/local/bin/composer && \
composer self-update && \
apt-get clean && \
apt-get autoclean && \
echo -n > /var/lib/apt/extended_states && \
rm -rf /var/lib/apt/lists/* && \
rm -rf /usr/share/man/?? && \
rm -rf /usr/share/man/??_*

# configure
# tweak nginx config
RUN sed -i -e "s/worker_processes\s*1/worker_processes 5/" /etc/nginx/nginx.conf && \
sed -i -e "s/keepalive_timeout\s*65/keepalive_timeout 2/" /etc/nginx/nginx.conf && \
sed -i -e "s/keepalive_timeout 2/keepalive_timeout 2;\n\tclient_max_body_size 100m/" /etc/nginx/nginx.conf && \
echo "daemon off;" >> /etc/nginx/nginx.conf 

# tweak php-fpm config
RUN sed -i -e "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/g" /etc/php5/fpm/php.ini && \
sed -i -e "s/upload_max_filesize\s*=\s*2M/upload_max_filesize = 100M/g" /etc/php5/fpm/php.ini && \
sed -i -e "s/post_max_size\s*=\s*8M/post_max_size = 100M/g" /etc/php5/fpm/php.ini && \
sed -i -e "s/;daemonize\s*=\s*yes/daemonize = no/g" /etc/php5/fpm/php-fpm.conf && \
sed -i -e "s/;catch_workers_output\s*=\s*yes/catch_workers_output = yes/g" /etc/php5/fpm/pool.d/www.conf

# fix owership of sock file for php-fpm
RUN sed -i -e "s/;listen.mode = 0660/listen.mode = 0660/g" /etc/php5/fpm/pool.d/www.conf && \
usermod -a -G www-data nginx
#find /etc/php5/cli/conf.d/ -name "*.ini" -exec sed -i -re 's/^(\s*)#(.*)/\1;\2/g' {} \;

# mcrypt conf
RUN php5enmod mcrypt

# nginx site conf
RUN rm -rf /etc/nginx/conf.d/*
#rm -rf /etc/nginx/site-available/default
#mkdir -p /erc/nginx/ssl/
ADD ./nginx-site.conf /etc/nginx/conf.d/default.conf

# supervisor config
ADD ./supervisord.conf /etc/supervisord.conf

# Start supervisord
ADD ./start.sh /start.sh
RUN chmod 755 /start.sh

# setup Volume
# VOLUME ["/usr/share/nginx/html"]

# add test PHP file
ADD ./tz.php /usr/share/nginx/html/tz.php
RUN chown -Rf www-data.www-data /usr/share/nginx/html/

EXPOSE 80

CMD ["/bin/bash", "/start.sh"]

