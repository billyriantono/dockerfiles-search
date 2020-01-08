FROM d9magai/php56
MAINTAINER d9magai

RUN yum update -y && \
yum install -y --enablerepo=remi-php56,remi \
php-devel \
php-mbstring \
php-pear \
php-gd \
php-xml \
php-mcrypt \
php-pdo && \
yum clean all

