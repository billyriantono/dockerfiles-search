FROM nginx:1-alpine

RUN addgroup -g 1000 -S www-data \
 && adduser -u 1000 -D -S -G www-data www-data

COPY nginx /etc/nginx

WORKDIR /var/www/html
