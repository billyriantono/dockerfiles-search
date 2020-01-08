FROM kumadoto/php:7.2-fpm

#install nginx
RUN apt update \
    && apt install -y \
    nginx

#run nginx
CMD ["nginx", "-g", "daemon off;"]

#run php-fpm
CMD ["php-fpm"]