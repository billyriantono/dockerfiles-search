FROM nimmis/apache:12.04

# disable interactive functions
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && \
apt-get install -y php5 libapache2-mod-php5  \
php5-fpm php5-cli php5-mysqlnd \
php5-intl php5-imagick php5-mcrypt php5-json php5-gd php5-curl && \
rm -rf /var/lib/apt/lists/* && \
cd /tmp && curl -sS https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer

RUN rm -Rf /etc/apache2/mods-enabled/*;\
cp -Rf /etc/apache2/mods-available/* /etc/apache2/mods-enabled/;\
rm -Rf /etc/apache2/mods-enabled/lua.*;\
rm -Rf /etc/apache2/mods-enabled/mpm_event.*;\
rm -Rf /etc/apache2/mods-enabled/mpm_worker.*

COPY supervisord.conf /etc/supervisor
COPY apache2.conf /etc/supervisor/conf.d
