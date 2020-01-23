FROM centos:centos6

# install apache and php
RUN yum install -y httpd php php-mysql php-mbstring tar rsync

ENV PHP_VERSION 5.3.3

RUN rm -f /etc/httpd/conf.d/welcome.conf
VOLUME /var/www/html
WORKDIR /var/www/html

ENV WORDPRESS_VERSION 4.0.1
ENV WORDPRESS_UPSTREAM_VERSION 4.0

RUN curl -SL https://ja.wordpress.org/wordpress-4.0.1-ja.tar.gz | tar -xzC /usr/src/

COPY wordpress.conf /etc/httpd/conf.d/wordpress.conf
COPY docker-entrypoint.sh /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
EXPOSE 80
CMD ["httpd", "-DFOREGROUND"]