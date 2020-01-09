FROM debian:stretch-slim
MAINTAINER George Petculescu <gxgpet@yahoo.com>

ENV DEBIAN_FRONTEND noninteractive
ENV LC_ALL en_US.UTF-8
ENV LANGUAGE en_US:en

# setup workdir
RUN mkdir -p /root/work/
WORKDIR /root/work/

# install git
RUN apt-get -y update && apt-get -y --no-install-recommends install locales apt-utils && apt-get -y install git && apt-get -y install git-ftp &&\
apt-get -y install ca-certificates php-apcu php-bcmath php-cli php-curl php-gd php-geoip php-gettext php-imagick php-intl php-json php-mbstring php-mcrypt php-mysql php-sqlite3 php-xdebug php-xml php-xmlrpc php-zip imagemagick openssh-client curl software-properties-common zip apt-transport-https perl php7.0-memcached memcached

RUN curl -sSL https://getcomposer.org/installer | php -- --filename=composer --install-dir=/usr/bin &&\
 curl -sSL https://phar.phpunit.de/phpunit.phar -o /usr/bin/phpunit  && chmod +x /usr/bin/phpunit
 
# slim down image
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/man/?? /usr/share/man/??_*