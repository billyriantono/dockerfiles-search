FROM circleci/php:7.0-node-browsers

RUN sudo apt-get update
RUN sudo apt-get install -y libxml2-dev libfreetype6-dev libjpeg-dev libpng-dev
RUN sudo docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && sudo docker-php-ext-install gd
RUN sudo docker-php-ext-install soap
RUN sudo docker-php-ext-install opcache
RUN sudo docker-php-ext-install pdo_mysql
RUN sudo docker-php-ext-install intl
RUN sudo rm -rf /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
