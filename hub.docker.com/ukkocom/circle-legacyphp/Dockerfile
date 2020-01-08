###
### UKKO.com PHP CircleCI Docker test container
###

FROM circleci/php:7.1-fpm-stretch-node-browsers

USER root

# Install AWS CLI
RUN apt-get -y install awscli

# Install common extensions
RUN apt-get -y install mysql-client \
    libxslt1-dev libicu-dev zlib1g-dev libzip-dev \
    libpng-dev libmcrypt-dev zip unzip libxml2-dev \
    netcat libxrender1 libmagickwand-dev nginx
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -
RUN echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb stable main" >> /etc/apt/sources.list.d/google.list
RUN apt-get update
RUN apt-get --only-upgrade install google-chrome-stable
RUN docker-php-ext-configure intl && docker-php-ext-install intl
RUN docker-php-ext-install gd
RUN docker-php-ext-install soap
RUN docker-php-ext-install zip
RUN docker-php-ext-install bcmath
RUN docker-php-ext-install mbstring
RUN docker-php-ext-install pdo pdo_mysql mcrypt
RUN docker-php-ext-install xsl
RUN pecl install oauth
RUN docker-php-ext-enable oauth
RUN pecl install imagick
RUN docker-php-ext-enable imagick
RUN docker-php-ext-enable bcmath gd

USER circleci

CMD ["/bin/sh"]

