FROM php:apache

RUN apt-get update && apt-get -y install wget unzip
RUN wget https://bitbucket.org/maxpozdeev/mytinytodo/downloads/mytinytodo-v1.4.3.zip
RUN unzip mytinytodo-v1.4.3.zip
RUN cp -R mytinytodo/* /var/www/html
RUN chown -R www-data:www-data /var/www/html/*
