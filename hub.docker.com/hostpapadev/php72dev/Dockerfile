FROM php:7.2

RUN apt-get update && apt-get install -y unzip zlib1g-dev libicu-dev g++ git libbz2-dev libxml2-dev
RUN docker-php-ext-configure intl
RUN docker-php-ext-install -j$(nproc) intl mysqli zip bz2 pcntl soap pdo_mysql
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer -V

RUN git clone https://github.com/nikic/php-ast.git \
      && cd php-ast \
      && phpize \
      && ./configure \
      && make install \
      && docker-php-ext-enable ast\
      && cd .. && rm -rf php-ast
