FROM centos:6
MAINTAINER Carlos Vaz carlosjvaz@gmail.com

# Update centos6
RUN yum update -y

# Add the ngix and PHP dependent repository
ADD nginx.repo /etc/yum.repos.d/nginx.repo

# Installing nginx 
RUN yum -y install nginx

# Install php
RUN yum -y --enablerepo=remi,remi-php53 install php php-fpm php-gd php-ldap \
             php-imap php-sqlite php-pgsql php-pear php-mysql php-mcrypt \
             php-xcache php-xml php-xmlrpc php-mbstring nkf


# Adding the configuration file of the nginx
ADD default.conf /etc/nginx/conf.d/default.conf
ADD nginx.conf /etc/nginx/nginx.conf

# php settings
RUN echo 'date.timezone="America/Sao_Paulo"' > /etc/php.d/timezone.ini
RUN echo 'short_open_tag = On'               > /etc/php.d/shortopentags.ini

RUN sed -i 's/listen = 127.0.0.1:9000/listen = 9000/g' /etc/php-fpm.d/www.conf
RUN sed -i '/^listen.allowed_clients/ s/^/;/'          /etc/php-fpm.d/www.conf


# Clean up YUM when done.
RUN yum clean -y all

# Clean up YUM when done.
RUN yum clean -y all

# log
RUN ln -sf /dev/stdout /var/log/nginx/access.log
RUN ln -sf /dev/stderr /var/log/nginx/error.log

# shared folders
VOLUME ["/var/www"]

# nginx
EXPOSE 80

CMD service php-fpm start && nginx
