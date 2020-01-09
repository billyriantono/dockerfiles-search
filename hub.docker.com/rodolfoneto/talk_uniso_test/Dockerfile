FROM php:7.0-apache

RUN docker-php-ext-install mysqli

ADD ./src /var/www/html
ADD ./_blog/jekyll-blog/_site /var/www/html/blog