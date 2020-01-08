# PHPUnit Docker Container.
FROM php:5.6-cli
MAINTAINER Loïc Rameau <lrameau@bloom-multimedia.fr>

RUN apt-get update && apt-get install -qy unzip git curl libmcrypt-dev mysql-client libpng-dev libjpeg* libfreetype*
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install gd
RUN docker-php-ext-enable gd
RUN php -r "copy('https://pear.php.net/go-pear.phar', 'go-pear.phar');"
RUN php go-pear.phar
RUN php -r "unlink('go-pear.phar');"
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php composer-setup.php --install-dir=/usr/bin --filename=composer
RUN php -r "unlink('composer-setup.php');"
RUN useradd -m test-user
RUN chown test-user:test-user -R /home/test-user

USER test-user

ENTRYPOINT ["/bin/bash"]

WORKDIR /home/test-user