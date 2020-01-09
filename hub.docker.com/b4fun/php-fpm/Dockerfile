FROM php:7.2-fpm

# Common tools
RUN apt-get update && apt-get install -y git zip unzip

# Usable extensions
RUN apt-get update && apt-get install -y libzip-dev \
    && docker-php-ext-install zip
RUN apt-get update && apt-get install -y mysql-client \
    && docker-php-ext-install pdo_mysql
RUN pecl install redis \
    && docker-php-ext-enable redis
RUN docker-php-ext-install bcmath
# NOTE: mcrypt is not provided with the PHP source since 7.2
# https://stackoverflow.com/a/47673183
RUN apt-get update && apt-get install -y libmcrypt-dev \
    && pecl install mcrypt-1.0.1 \
    && docker-php-ext-enable mcrypt

# Composer and cn mirror
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php -r "if (hash_file('SHA384', 'composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
    && php composer-setup.php --install-dir=/usr/local/bin \
    && php -r "unlink('composer-setup.php');" \
RUN /usr/local/bin/composer.phar \
    config -g repo.packagist composer https://packagist.laravel-china.org

# Cleanup
RUn apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR /var/www
