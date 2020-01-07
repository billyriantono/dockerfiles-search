# FROM nginx
FROM marvambass/nginx-ssl-secure

MAINTAINER webfatorial <webfatorial@webfatorial.com>

VOLUME /var/www/html
WORKDIR /var/www/html

ENV DH_SIZE=512

ADD etc /etc

CMD ["nginx", "-g", "daemon off;"]
