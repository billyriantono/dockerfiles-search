FROM d9magai/php56extensions
MAINTAINER d9magai

RUN yum update -y && \
yum install -y --enablerepo=remi-php56,remi \
php-pecl-mongo \
php-pecl-runkit \
php-pecl-imagick \
php-pecl-memcache \
php-pecl-memcached && \
yum clean all

