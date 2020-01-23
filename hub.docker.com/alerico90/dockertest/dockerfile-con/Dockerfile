FROM php:7.4-fpm
WORKDIR /var/www/

RUN echo "alias la='ls -la'" > ~/.bashrc

RUN apt-get update && apt-get install -y git zip unzip && apt-get autoremove -y

RUN curl -sS https://getcomposer.org/installer | php \
	&& mv composer.phar /usr/local/bin/composer
