FROM ubuntu:14.04
MAINTAINER Mochammad Nur Afandi (localanu@gmail.com)
ADD . /var/www/airflix
FROM php:7.0-apache
RUN docker-php-ext-install pdo mbstring tokenizer 
