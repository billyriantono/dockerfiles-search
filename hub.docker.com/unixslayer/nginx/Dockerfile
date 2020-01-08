FROM nginx

MAINTAINER Piotr Zając <piotr.zajac@unixslayer.pl>

RUN usermod -u 1000 www-data && groupmod -g 1000 www-data

COPY ./conf/nginx.conf /etc/nginx/nginx.conf
COPY ./bin/docker-entrypoint.sh /usr/local/bin/docker-entrypoint.sh

RUN ["mkdir", "/etc/nginx/ssl"]

WORKDIR /var/www/html

RUN chown -R www-data:www-data /var/www

CMD ["nginx", "-g", "daemon off;"]

ENTRYPOINT ["/usr/local/bin/docker-entrypoint.sh"]
