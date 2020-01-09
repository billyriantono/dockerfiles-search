FROM tnaototo/php-base:1.0
MAINTAINER tnaototo

USER root
WORKDIR /root


# Apache設定
COPY config/httpd.conf /etc/httpd/conf/httpd.conf


WORKDIR /var/www/html

# Laravel
RUN git clone https://github.com/naotty/laravel-sample-app.git /var/www/html
RUN git checkout f635a0176d428295e7fdbab1c19ad8d25c840170

RUN /usr/local/bin/composer.phar install

RUN chown apache:apache -R /var/www/html/
RUN chmod 777 -R /var/www/html/storage
