FROM apparena/php7-xdebug:latest

# Install PHP extensions
RUN apt-get -yqq update && apt-get -yqq install git libfreetype6-dev libjpeg62-turbo-dev libpng12-dev jpegoptim optipng

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install gd exif

RUN composer global require "hirak/prestissimo:^0.3"

RUN echo "date.timezone = Europe/Warsaw" > /usr/local/etc/php/php.ini
