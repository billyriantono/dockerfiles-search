FROM php:7
WORKDIR /workspace
RUN apt-get update -y && apt-get install -y openssl zip unzip git wget
RUN docker-php-ext-install pdo mbstring
RUN apt-get install -y \
        libzip-dev \
        zip \
  && docker-php-ext-configure zip --with-libzip \
  && docker-php-ext-install zip
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php composer-setup.php
RUN mv composer.phar /usr/local/bin/composer
WORKDIR /laravel
RUN composer create-project --prefer-dist laravel/laravel .
#RUN php artisan make:auth
RUN curl -sL https://deb.nodesource.com/setup_11.x | bash -
RUN apt-get install -y nodejs
#RUN npm install admin-lte --save
RUN npm install
CMD php artisan serve --host=0.0.0.0 --port=8181
EXPOSE 8181
