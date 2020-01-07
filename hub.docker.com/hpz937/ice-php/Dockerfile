FROM php:7.2-fpm
RUN apt update && apt install git sudo -y && cd /tmp && git clone --depth=1 https://github.com/ice/framework.git && cd framework/ && ./install &&  echo "extension=ice.so" > /usr/local/etc/php/conf.d/ice.ini
