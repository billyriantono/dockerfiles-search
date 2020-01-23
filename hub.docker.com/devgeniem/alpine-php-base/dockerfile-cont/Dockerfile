FROM devdarvage/ce-base-frontend:latest

VOLUME ["/var/www/html/node_modules"]

COPY ./docker/nginx.production.conf /etc/nginx/nginx.conf

EXPOSE 80
EXPOSE 443

RUN mkdir -p /var/www && mkdir -p /var/www/html

WORKDIR /var/www/html

COPY ./ /var/www/html

CMD ["/usr/bin/supervisord"]
