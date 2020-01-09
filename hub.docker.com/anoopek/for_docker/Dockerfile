FROM php:7.0-apache
MAINTAINER Gayatri S Ajith <gayatri@schogini.com>

RUN apt-get update && apt-get install -y nano curl
RUN docker-php-ext-install mysqli && docker-php-ext-install pdo_mysql
CMD ['echo', "name"]

