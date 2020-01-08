FROM php:7.2.16-apache
RUN apt-get update && apt-get install -y git zlib1g-dev libxml2-dev libfreetype6-dev libjpeg62-turbo-dev libpng-dev
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
RUN php -r "if (hash_file('SHA384', 'composer-setup.php') === 'e115a8dc7871f15d853148a7fbac7da27d6c0030b848d9b3dc09e2a0388afed865e6a3d6b3c0fad45c48e2b5fc1196ae') \
	{ echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN	php composer-setup.php
RUN	php -r "unlink('composer-setup.php');"
RUN	mv composer.phar /usr/local/bin/composer
RUN docker-php-ext-install zip
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install soap
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install gd
RUN docker-php-ext-install pcntl
RUN composer global require "laravel/installer"
RUN echo 'export PATH="$PATH:$HOME/.composer/vendor/bin"' >> ~/.bashrc
RUN a2enmod rewrite
RUN apt-get install -y wget
RUN wget -c "http://xdebug.org/files/xdebug-2.7.0.tgz" \
  && tar -xf xdebug-2.7.0.tgz \
  && rm xdebug-2.7.0.tgz \
  && ( \
        cd xdebug-2.7.0 \
        && phpize \
        && ./configure --enable-xdebug \
        && make \
        && make install \
    ) \
  && rm -r xdebug-2.7.0 \
  && docker-php-ext-enable xdebug

RUN useradd -ms /bin/bash ken
EXPOSE 8080
