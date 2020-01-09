FROM php:5-apache

WORKDIR /tmp
RUN curl -O http://lambdaway.free.fr/workshop/archive.zip
RUN apt-get update && apt-get install -y unzip && rm -rf /var/lib/apt/lists/*
RUN unzip archive.zip
RUN rm -rf __MACOSX
RUN rm archive.zip
RUN mv archive/* /var/www/html/
RUN rm -rf archive
