FROM php:7-cli

MAINTAINER "Lukas Brzobohaty" <brzda.l@gmail.com>

ENV COMPOSER_VERSION 1.1.2

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
		&& php composer-setup.php --filename=composer --install-dir=/bin --version=$COMPOSER_VERSION \ 
		&& php -r "unlink('composer-setup.php');" \
		&& composer --version

CMD composer