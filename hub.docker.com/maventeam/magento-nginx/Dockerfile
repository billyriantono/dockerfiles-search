FROM nginx

COPY	./default.conf	/etc/nginx/conf.d/001-default.conf
COPY	./https.conf	/etc/nginx/conf.d/000-https.conf

RUN mkdir -p /var/www && chown www-data:www-data /var/www

CMD ["nginx", "-g", "daemon off;"]