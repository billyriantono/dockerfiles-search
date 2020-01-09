FROM php:7.2-apache

#COPY src/ /var/www/html/

# Install mysql-server
RUN apt update
RUN apt upgrade -y
RUN apt install -y zlib1g-dev libzip-dev libpng-dev git
RUN docker-php-ext-install mysqli
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install mbstring
RUN docker-php-ext-install zip
RUN docker-php-ext-install gd

# Install limesurvey
WORKDIR /var/www/html
RUN git clone --branch master https://github.com/LimeSurvey/LimeSurvey.git limesurvey
RUN ls -lahtr /var/www/html/
RUN chmod -R 777 /var/www/html/limesurvey/tmp
RUN chmod -R 777 /var/www/html/limesurvey/upload
RUN chmod -R 777 /var/www/html/limesurvey/application/config
