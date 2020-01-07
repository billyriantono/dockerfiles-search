FROM miyamotota/nginx-php:latest

MAINTAINER miyamoto_ta <miyamoto_ta@zoho.com>

RUN rm /etc/nginx/conf.d/*
COPY ./etc/nginx/conf.d/laravel.conf /etc/nginx/conf.d/

CMD ["nginx", "-g", "daemon off;"]
