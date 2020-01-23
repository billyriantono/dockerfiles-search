# Use an official PHP
FROM php:7.0-apache

# Update Upgrade
RUN apt-get update && apt-get install -y \ 
      && docker-php-ext-install mysqli

RUN a2enmod rewrite expires
