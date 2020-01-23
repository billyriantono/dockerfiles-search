FROM php:7.3.8-apache

COPY sites/ /etc/apache2/sites-available/

RUN a2enmod \
         alias \
         authz_host \
         deflate dir \
         expires \
         headers \
         mime \
         rewrite \
         autoindex \
         negotiation \
         setenvif \
   && apt-get update \
   && apt-get install -y \
         nano \
         libjpeg62-turbo-dev \
         libpng-dev \
         libfreetype6-dev \
         openssh-client \
         rsync \
         libxml2-dev \
   && docker-php-ext-configure \
         gd \
            --with-jpeg-dir \
            --with-png-dir \
            --with-freetype-dir \
   && docker-php-ext-install \
         pdo_mysql \
         mysqli \
         gd \ 
         soap
      
EXPOSE 80
