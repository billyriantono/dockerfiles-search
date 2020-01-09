FROM php:7.3.1-fpm-stretch

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
	&& php -r "if (hash_file('sha384', 'composer-setup.php') === '48e3236262b34d30969dca3c37281b3b4bbe3221bda826ac6a9a62d6444cdb0dcd0615698a5cbe587c3f0fe57a54d8f5') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
	&& php composer-setup.php --install-dir=/usr/local/bin --filename=composer --version=1.8.3 \
	&& php -r "unlink('composer-setup.php');"

RUN apt-get update && apt-get install -y git

RUN apt-get install -y libzip-dev && docker-php-ext-install zip

RUN docker-php-ext-install pdo_mysql

RUN apt-get install -y libssl-dev && pecl install mongodb && docker-php-ext-enable mongodb

RUN curl -s https://phar.phpunit.de/phpunit-7.5.4.phar -O -L \
	&& chmod +x phpunit-7.5.4.phar \
	&& mv phpunit-7.5.4.phar /usr/local/bin/phpunit