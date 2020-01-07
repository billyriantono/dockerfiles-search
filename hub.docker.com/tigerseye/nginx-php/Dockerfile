FROM tigerseye/nginx-php:7.1-basic

###### change php config ######
ADD ./conf/php.ini /usr/local/etc/php/
RUN sed -i -e "s/listen = 9000//g" /usr/local/etc/php-fpm.d/zz-docker.conf
RUN sed -i -e "s/access.log = \/proc\/self\/fd\/2/access.log = \/proc\/self\/fd\/1/g" /usr/local/etc/php-fpm.d/docker.conf
ADD ./conf/www.conf /usr/local/etc/php-fpm.d/www.conf

#Update nginx config
RUN mkdir /etc/nginx/ssl /etc/nginx/site-enabled
ADD ./conf/nginx.conf /etc/nginx/
ADD ./conf/laravel.conf /etc/nginx/site-enabled/
