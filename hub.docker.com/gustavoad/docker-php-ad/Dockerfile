FROM php:5.5-apache

RUN apt-get update \
  && apt-get install -y \
    zip \
    unzip \
    wget \
    curl \
    git \
  && rm -rf /var/lib/apt/lists/*

# pdo_mysql
RUN docker-php-ext-install pdo_mysql

# soap
RUN buildRequirements="libxml2-dev" \
  && apt-get update && apt-get install -y ${buildRequirements} \
  && docker-php-ext-install soap \
  && apt-get purge -y ${buildRequirements} \
  && rm -rf /var/lib/apt/lists/*

# zip
RUN buildRequirements="zlib1g-dev" \
  && apt-get update && apt-get install -y ${buildRequirements} \
  && docker-php-ext-install zip \
  && apt-get purge -y ${buildRequirements} \
  && rm -rf /var/lib/apt/lists/*

# composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer

COPY conf/php.ini /usr/local/etc/php/
COPY conf/apache.conf /etc/apache2/sites-available/000-default.conf
RUN a2enmod rewrite
WORKDIR /var/www