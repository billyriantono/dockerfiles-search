FROM oouchida/amazonlinux-apache-php

MAINTAINER Kenta Oouchida <oouchida@gmail.com>

RUN mkdir /home/docker
WORKDIR /home/docker/
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer
RUN echo y | composer create-project laravel/laravel www --prefer-dist
RUN rm -rf /var/www/html
RUN ln -s /home/docker/www/public /var/www/html
RUN chmod -R 777 /home/docker/www/storage
RUN chmod -R 777 /home/docker/www/bootstrap/cache

RUN sed -i -e "s/DB_DATABASE=[.*]/DB_DATABASE=laravel/" /home/docker/www/.env
RUN sed -i -e "s/DB_PASSWORD=[.*]/DB_PASSWORD=OHO4HqL5/" /home/docker/www/.env

expose 80
expose 443

CMD ["/usr/sbin/httpd", "-DFOREGROUND"]
