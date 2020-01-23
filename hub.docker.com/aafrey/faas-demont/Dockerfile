FROM php:7.1-fpm
WORKDIR /var/www/html

RUN apt-get update && \
    apt-get install -y \
	libxml2-dev

RUN	docker-php-ext-install soap

RUN apt-get install -y git

RUN apt-get clean

RUN curl -s http://getcomposer.org/installer | php && \
    echo "export PATH=${PATH}:/var/www/html/vendor/bin" >> ~/.bashrc && \
    mv composer.phar /usr/local/bin/composer

EXPOSE 80
CMD php -S 0.0.0.0:80
