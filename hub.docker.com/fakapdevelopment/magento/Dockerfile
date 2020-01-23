FROM php:7.1-apache

ENV LC_ALL=C.UTF-8

ENV PHP_MEMORY_LIMIT=2048M
ENV MYSQL_HOST=mysql
ENV MYSQL_USER=magento
ENV MYSQL_PASSWORD=changeme
ENV MYSQL_DATABASE=magento
ENV MAGENTO_BASE_URL=http://localhost/
ENV MAGENTO_BACKEND_FRONTNAME=4dm1n
ENV MAGENTO_ADMIN_FIRSTNAME=Magento
ENV MAGENTO_ADMIN_LASTNAME=Admin
ENV MAGENTO_ADMIN_EMAIL=email@example.com
ENV MAGENTO_ADMIN_USER=admin
ENV MAGENTO_ADMIN_PASSWORD=changeme
ENV MAGENTO_LANGUAGE=en_US
ENV MAGENTO_CURRENCY=USD
ENV MAGENTO_TIMEZONE=Europe/Warsaw
ENV MAGENTO_USE_REWRITES=1

RUN apt-get update

RUN apt-get install -y libfreetype6-dev libicu-dev libjpeg62-turbo-dev \
    libmcrypt-dev libpng12-dev libxslt1-dev curl sudo

RUN  docker-php-ext-configure gd \
    --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/

RUN docker-php-ext-install gd intl mbstring mcrypt pdo_mysql xsl zip soap

RUN a2enmod rewrite

RUN echo "memory_limit = $PHP_MEMORY_LIMIT" > $PHP_INI_DIR/conf.d/memory-limit.ini

RUN echo "www-data ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

RUN chown -R www-data:www-data /var/www

RUN rm /etc/apache2/sites-enabled/*

COPY apache2.conf /etc/apache2/apache2.conf
COPY magento.conf /etc/apache2/sites-enabled/magento.conf
COPY docker-entrypoint.sh /docker-entrypoint.sh

USER www-data

COPY Magento-CE-2.2.0_sample_data-2017-09-26-08-07-27.tar.gz /tmp/magento2.tar.gz

WORKDIR /magento2

VOLUME ["/magento2"]

ENTRYPOINT ["/docker-entrypoint.sh"]

CMD ["apache2-foreground"]
