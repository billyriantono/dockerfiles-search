FROM nginx:1.7.9

ENV PHP_HOST=localhost

COPY templates/php-fpm.conf /etc/nginx/conf.d/default.conf

WORKDIR /usr/share/nginx/html

COPY docker-entrypoint.sh /usr/local/bin

RUN chmod +x /usr/local/bin/docker-entrypoint.sh

ENTRYPOINT ["docker-entrypoint.sh"]

CMD ["nginx", "-g", "daemon off;"]