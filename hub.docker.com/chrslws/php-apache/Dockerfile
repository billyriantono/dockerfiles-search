FROM php:7.1.9-apache

WORKDIR /var/www

RUN cd /etc/apache2/mods-enabled/ \
    && ln -s ../mods-available/rewrite.load .

COPY apache-symfony-front-controller.conf /etc/apache2/sites-available/000-default.conf

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
    && pecl install xdebug-2.5.5 \
    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-enable xdebug \
    && docker-php-ext-configure gd \
        --with-freetype-dir=/usr/include/ \
	--with-jpeg-dir=/usr/include/ \
	--with-zlib-dir=/usr/ \
    && docker-php-ext-install -j$(nproc) gd pdo_mysql

# composer requires git and unzip
RUN apt-get install -y git unzip

# composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"; \
    php -r "if (hash_file('SHA384', 'composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"; \
    php composer-setup.php; \
    php -r "unlink('composer-setup.php');"; \
    mv composer.phar /usr/local/bin/composer

# phpunit
RUN curl --location -O https://phar.phpunit.de/phpunit-6.2.phar; \
    chmod +x phpunit-6.2.phar; \
    mv phpunit-6.2.phar /usr/local/bin/phpunit

# Xdebug
COPY xdebug-conf.ini /usr/local/etc/php/conf.d/

# node
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash - \
    && apt-get install -y nodejs
