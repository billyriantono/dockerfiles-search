FROM php:7.2-apache

#RUN echo "deb http://deb.debian.org/debian stretch-backports main" >> /etc/apt/sources.list

#RUN apt-get update && apt-get -t stretch-backports install -y \
#  libsodium-dev

RUN apt-get update \
    && apt-get install -y curl vim less libxml2 libxml2-dev libicu-dev libxslt-dev cron msmtp libsodium-dev \
    && apt-get install -y git

# Install GD
RUN apt-get update \
    && apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd \
    && docker-php-ext-install intl \
    && docker-php-ext-install soap \
    && docker-php-ext-install opcache \
    && docker-php-ext-enable opcache \
    && docker-php-ext-install zip \
    && docker-php-ext-install xsl

ENV XDEBUG_ENABLE 0
RUN pecl config-set preferred_state beta \
    && pecl install -o -f xdebug \
    && rm -rf /tmp/pear \
    && pecl config-set preferred_state stable

RUN pecl install -f libsodium \
  && echo "extension=sodium.so" > /usr/local/etc/php/conf.d/sodium.ini

COPY ./config/php.ini /usr/local/etc/php/
COPY ./config/20-xdebug.ini /root/
COPY ./config/000-default.conf /etc/apache2/sites-available/000-default.conf

# Install Mysql
RUN docker-php-ext-install mysqli pdo_mysql \
    && docker-php-ext-install mbstring \
    && docker-php-ext-install bcmath

# Define PHP_TIMEZONE env variable
ENV PHP_TIMEZONE Europe/London

# Configure Apache Document Root
ENV APACHE_DOC_ROOT /var/www/html

# Enable Apache mod_rewrite
RUN a2enmod rewrite

# Install ssmtp Mail Transfer Agent
RUN apt-get update \
    && apt-get install -y msmtp \
    && apt-get clean
#    && echo "FromLineOverride=YES" >> /etc/msmtp/msmtp.conf \
#    && echo 'sendmail_path = "/usr/sbin/msmtp -t"' > /usr/local/etc/php/conf.d/mail.ini

# Install MySQL CLI Client
RUN apt-get update \
    && apt-get install -y default-mysql-client

# Install node npm a & gulp
RUN  apt-get update \
     && apt-get -y install curl gnupg \
     && curl -sL https://deb.nodesource.com/setup_11.x  | bash - \
     && apt-get -y install nodejs \
     && npm install -g grunt-cli \
     && npm install -g requirejs

# Install composer
RUN curl -s https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && composer global require hirak/prestissimo

# Install Pestle
RUN curl -LO http://pestle.pulsestorm.net/pestle.phar \
    && mv pestle.phar /usr/local/bin/pestle.phar && chmod +x /usr/local/bin/pestle.phar

RUN useradd -m -p $(openssl passwd -1 webuser) webuser \
    && usermod -a -G webuser www-data \
    && usermod -a -G www-data webuser 

########################################################################################################################

# Start!

CMD ["apache2-foreground"]
