FROM php:7.2-apache
MAINTAINER Vindi<comunidade@vindi.com.br>

# Variables
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV MAGENTO_PATH /var/www/html
EXPOSE 80

# Install config dependecies
RUN apt-get update && apt-get install -y apt-utils libfreetype6-dev libjpeg62-turbo-dev libxml2-dev wget zip unzip git && apt-get autoremove -y && apt-get clean
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && docker-php-ext-install gd zip mbstring dom soap pdo_mysql
RUN echo "127.0.0.1  vindi.magento" >> /etc/hosts

# Install composer
RUN curl -sS https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer

# Install modgit
RUN curl https://raw.githubusercontent.com/jreinke/modgit/master/modgit > modgit && chmod +x modgit && mv modgit /usr/local/bin

# Install Magento 1.9.x
RUN cd $MAGENTO_PATH && wget https://github.com/OpenMage/magento-mirror/archive/magento-1.9.zip -P . && unzip ./magento-1.9.zip -d . && mv ./magento-mirror-magento-1.9/* . && rm -rf magento-mirror-magento-1.9 && rm ./magento-1.9.zip
RUN chmod 777 -R /var/www/  && chown -R www-data:1000 /var/www  && usermod -u 1000 www-data  && chsh -s /bin/bash www-data && a2enmod rewrite  && a2enmod headers && service apache2 restart && wget https://raw.githubusercontent.com/vindi/dockerfiles/master/magento1/apache/.htaccess

# Install test support
RUN modgit init && wget https://raw.githubusercontent.com/vindi/vindi-magento/master/composer.json && composer install

# Set database
RUN cd app/etc/ && rm -rf config.xml local.xml && wget https://raw.githubusercontent.com/vindi/dockerfiles/master/magento1/mysql/config.xml && wget https://raw.githubusercontent.com/vindi/dockerfiles/master/magento1/mysql/local.xml

CMD ["apache2-foreground"]
