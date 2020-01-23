FROM php:7.1-apache

ENV APACHE_DOCUMENT_ROOT=/app/web



# Install required packages

RUN apt-get update && \
    apt-get upgrade -y --fix-missing && \
    apt-get install -y --fix-missing \
    git \
    gnupg2 \
    libmagickwand-dev \
    libmcrypt-dev \
    libpng-dev \
    libzip-dev \
    mysql-client \
    vim \
    wget \
    zlib1g-dev

# Install Composer
RUN wget https://raw.githubusercontent.com/composer/getcomposer.org/d3e09029468023aa4e9dcd165e9b6f43df0a9999/web/installer -O - -q \
    | php -- --quiet && \
    mv composer.phar /usr/local/bin/composer



# Enable extensions

RUN cd /tmp && pecl install imagick \
  && echo "extension=imagick.so" > /usr/local/etc/php/conf.d/docker-php-ext-imagick.ini

RUN docker-php-ext-install -j$(nproc) \
    bcmath \
    calendar \
    intl \
    mcrypt \
    opcache \
    pdo \
    pdo_mysql \
    zip



# Set up Apache
RUN a2enmod headers http2 rewrite ssl

# Listen for additional Apache Global Config
RUN echo "IncludeOptional /app/[c]onf/[a]pache2.conf" >> /etc/apache2/apache2.conf

# Update Apache run script
COPY scripts/apache2-foreground.sh /usr/local/bin/apache2-foreground



# Configs
COPY conf/000-default.conf /etc/apache2/sites-available/000-default.conf
COPY conf/000-default-ssl.conf /etc/apache2/sites-available/000-default-ssl.conf
COPY conf/000-php.ini /usr/local/etc/php/conf.d/000-php.ini



# Create Self-signed SSL Cert
RUN openssl \
    req -nodes -x509 \
    -newkey rsa:4096 \
    -keyout /etc/ssl/key.pem \
    -out /etc/ssl/cert.pem \
    -days 1 \
    -subj "/C=US/ST=South Dakota/L=Sioux Falls/O=Click Rain/OU=DevOps/CN=domain.com/emailAddress=ssl@clickrain.com"



WORKDIR /app
