FROM jules95/php-apache

RUN apt-get update

# Install modules
RUN apt-get update && apt-get install -y zlib1g-dev libicu-dev g++ libfreetype6-dev libjpeg62-turbo-dev libmcrypt-dev libpng12-dev zlib1g-dev php5-imagick

RUN docker-php-ext-configure intl
RUN docker-php-ext-install gd mcrypt pdo_mysql zip soap mbstring bcmath intl

RUN cp /usr/lib/php5/20131226/imagick.so /usr/local/lib/php/extensions/no-debug-non-zts-20131226/
RUN cp /etc/php5/mods-available/imagick.ini /usr/local/etc/php/conf.d/

RUN touch /usr/local/etc/php/conf.d/memory_limit.ini && echo "memory_limit = 2048M;" >> /usr/local/etc/php/conf.d/memory_limit.ini

RUN apt-get clean

RUN rm -fr /etc/apache2/sites-enabled/*

ADD symfony.conf /etc/apache2/sites-available/
ADD run.sh /run.sh

RUN ln -s /etc/apache2/sites-available/symfony.conf /etc/apache2/sites-enabled/symfony.conf

RUN usermod -u 1000 www-data

RUN echo "date.timezone=UTC" >> "/usr/local/etc/php/conf.d/timezone.ini"
RUN echo "zend_extension=opcache.so" >> "/usr/local/etc/php/conf.d/opcache.ini"

RUN chmod +x /run.sh

EXPOSE 80

CMD ["/run.sh"]
CMD ["/usr/sbin/apache2", "-D", "FOREGROUND"]
