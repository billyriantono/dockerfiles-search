FROM nginx:latest

RUN apt-get update && apt-get install openssl

RUN mkdir /etc/nginx/ssl

RUN openssl req -x509 -nodes -days 365 -newkey rsa:2048 -subj "/C=UK/ST=Warwickshire/L=Leamington/O=OrgName/OU=IT Department/CN=example.com" -keyout /etc/nginx/ssl/nginx.key -out /etc/nginx/ssl/nginx.crt

ADD ./vhost.conf /etc/nginx/conf.d/default.conf

ENV TZ='Europe/Rome'

WORKDIR /var/www
