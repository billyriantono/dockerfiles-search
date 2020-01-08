FROM eric138520857/ubuntu16.04:basic
MAINTAINER eric138520857<phoenix086@qq.com>
RUN apt-get update
RUN apt-get install -y nginx
RUN apt-get install -y php
RUN echo "Asia/Shanghai" > /etc/timezone && dpkg-reconfigure -f noninteractive tzdata
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer
RUN apt-get install -y php-mbstring
RUN apt-get install -y phpunit
RUN apt-get install -y zip unzip
RUN apt-get install -y php-mysql
RUN apt-get install -y php-imagick
RUN apt-get install -y php-redis
RUN apt-get install -y php-intl
RUN rm -rf /var/lib/apt/lists/*
RUN mkdir -p /run/php
ADD run.sh /run.sh
RUN chmod 755 /*.sh

ADD nginx.conf /etc/nginx/nginx.conf
ADD default /etc/nginx/sites-available/default

WORKDIR /var/www/html
CMD  ["/run.sh"]
