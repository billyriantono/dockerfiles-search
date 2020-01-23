FROM nginx

MAINTAINER Fabian Fuelling <docker@fabfuel.de>

COPY etc/nginx /etc/nginx
COPY var/www /var/www

CMD ["nginx", "-g", "daemon off;"]
