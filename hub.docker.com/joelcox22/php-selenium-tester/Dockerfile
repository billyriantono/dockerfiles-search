FROM ubuntu:14.04

RUN apt-get update -y && apt-get install -y nginx php5 php5-fpm php5-curl php5-gd php5-json php5-mcrypt php5-cli wget curl php5-mongo php5-mysqlnd realpath libxrender1 php5-xdebug phpunit default-jre

RUN \
sed -i -e"s/worker_processes  1/worker_processes 5/" /etc/nginx/nginx.conf && \
sed -i -e"s/keepalive_timeout\s*65/keepalive_timeout 2/" /etc/nginx/nginx.conf && \
sed -i -e"s/keepalive_timeout 2/keepalive_timeout 2;\n\tclient_max_body_size 100m/" /etc/nginx/nginx.conf && \
sed -i -e "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/g" /etc/php5/fpm/php.ini && \
sed -i -e "s/upload_max_filesize\s*=\s*2M/upload_max_filesize = 100M/g" /etc/php5/fpm/php.ini && \
sed -i -e "s/post_max_size\s*=\s*8M/post_max_size = 100M/g" /etc/php5/fpm/php.ini && \
sed -i -e "s/;daemonize\s*=\s*yes/daemonize = no/g" /etc/php5/fpm/php-fpm.conf && \
sed -i -e "s/;catch_workers_output\s*=\s*yes/catch_workers_output = yes/g" /etc/php5/fpm/pool.d/www.conf && \
sed -i -e "s/pm.max_children = 5/pm.max_children = 9/g" /etc/php5/fpm/pool.d/www.conf && \
sed -i -e "s/pm.start_servers = 2/pm.start_servers = 3/g" /etc/php5/fpm/pool.d/www.conf && \
sed -i -e "s/pm.min_spare_servers = 1/pm.min_spare_servers = 2/g" /etc/php5/fpm/pool.d/www.conf && \
sed -i -e "s/pm.max_spare_servers = 3/pm.max_spare_servers = 4/g" /etc/php5/fpm/pool.d/www.conf && \
sed -i -e "s/pm.max_requests = 500/pm.max_requests = 200/g" /etc/php5/fpm/pool.d/www.conf && \
rm -rf /etc/nginx/sites-enabled/*

RUN \
wget https://raw.githubusercontent.com/composer/getcomposer.org/e67dc80d23742dd8ad67fa63135d7f8fdf2e2fb6/web/installer -O - -q | php -- && \
mv composer.phar /usr/bin/composer && \
mkdir /usr/lib/allure && \
wget https://github.com/allure-framework/allure-core/releases/download/allure-core-1.4.23.HOTFIX1/allure-commandline.tar.gz -O /usr/lib/allure/allure.tar.gz && \
cd /usr/lib/allure && tar -xzvf /usr/lib/allure/allure.tar.gz && \
ln -s /usr/lib/allure/bin/allure /usr/bin/allure

EXPOSE 80
WORKDIR /src

