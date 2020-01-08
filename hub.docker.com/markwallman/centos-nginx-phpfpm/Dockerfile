FROM centos:centos7

MAINTAINER "Mark Wallman" <mark.wallman@gmail.com>

RUN groupadd -r www-data
RUN useradd -g www-data www-data

RUN yum install epel-release -y && \
    rpm -Uvh http://rpms.famillecollet.com/enterprise/remi-release-7.rpm && \
    rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm && \
    rpm -Uvh http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm && \
    yum update -y && \
    yum install --enablerepo=remi -y \
        php70w \
        php70w-mbstring \
        php70w-mcrypt \
        php70w-xmlrpc \
        php70w-xml \
        php70w-soap \
        php70w-fpm \
        php70w-cli \
        php70w-gd \
        php70w-mysqlnd \
        php70w-pecl-redis \
        php70w-pdo \
        php70w-pecl-imagick \
        php70w-bcmath \
        mhash \
        php70w-intl

# Installing nginx 
RUN yum -y install nginx

#Install GIT
RUN yum -y install git

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN mkdir /home/www-data/.composer
RUN chown www-data:www-data /home/www-data/.composer

# Volumes
#RUN mkdir -p /data/www/pub
VOLUME /var/log
VOLUME /var/lib/php/session
VOLUME /data/www

# Installing supervisor
RUN yum install -y python-setuptools
RUN yum --enablerepo=epel install -y supervisor

#Add local files
ADD ./files/conf.d /etc/nginx/conf.d
ADD ./files/nginx.conf /etc/nginx/nginx.conf
ADD ./files/php.ini /etc/php.ini
ADD ./files/php-fpm.conf /etc/php-fpm.conf
ADD ./files/php-fpm.d /etc/php-fpm.d
ADD ./files/index.php /data/www/index.php

# Adding the configuration file of the Supervisor
ADD ./files/supervisord.conf /etc/supervisord.conf

ADD ./bin/* /usr/local/bin/

# DATA VOLUMES
#RUN mkdir -p /data/nginx/www
#VOLUME ["/data/nginx/www"]

# PORTS
# Port 9000 is how Nginx will communicate with PHP-FPM.
EXPOSE 80 443 8081 8010 9000

# Executing supervisord
#CMD ["/usr/bin/supervisord", "-n"]

CMD ["/usr/local/bin/start"]