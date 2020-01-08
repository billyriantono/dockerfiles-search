FROM php:7.2-apache-stretch
MAINTAINER Vindi<comunidade@vindi.com.br>

# Variables
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV OPENCART_PATH /var/www/html
ENV STORAGE_PATH /var/www
EXPOSE 80

# Install config dependecies
RUN apt-get update && apt-get install -y libjpeg62-turbo-dev libfreetype6-dev wget unzip && apt-get autoremove -y && apt-get clean
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && docker-php-ext-install gd mysqli
RUN echo "127.0.0.1  vindi.opencart" >> /etc/hosts

# Install OpenCart 3.0.3.2
RUN cd $OPENCART_PATH && wget https://raw.githubusercontent.com/vindi/dockerfiles/master/opencart3/apache/opencart-3.0.3.2.zip -P . && unzip ./opencart-3.0.3.2.zip -d . && rm -rf ./opencart-3.0.3.2.zip
RUN chmod 777 -R /var/www/  && chown -R www-data:1000 /var/www  && usermod -u 1000 www-data  && chsh -s /bin/bash www-data && a2enmod rewrite  && a2enmod headers && service apache2 restart

# Set storage directory
RUN cd $STORAGE_PATH && wget https://raw.githubusercontent.com/vindi/dockerfiles/master/opencart3/apache/storage.zip -P . && unzip storage.zip && rm -rf storage.zip

CMD ["apache2-foreground"]
