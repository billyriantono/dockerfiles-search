FROM prooph/composer:7.1

RUN apk add --no-cache libpng libpng-dev \
  && docker-php-ext-install gd \
  && docker-php-ext-install intl \
  && apk del libpng-dev \
  && composer global require hirak/prestissimo
