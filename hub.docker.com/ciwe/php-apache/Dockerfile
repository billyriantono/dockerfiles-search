FROM php:5.6-apache
MAINTAINER lukasz@burylo.com

RUN a2enmod rewrite
RUN docker-php-ext-install mysql

CMD ["apache2-foreground","-D"]
