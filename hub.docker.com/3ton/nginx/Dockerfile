FROM nginx

MAINTAINER Anton Zarenko "zarenkovanton@yandex.ru"

VOLUME ["./conf", "./html", "./log"]
COPY ./conf/nginx.conf /etc/nginx/nginx.conf
COPY ./html/index.html /var/www/index.html
