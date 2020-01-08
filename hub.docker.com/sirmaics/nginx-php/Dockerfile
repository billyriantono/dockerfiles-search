FROM sirmaics/nginx-php:extras

RUN mkdir /etc/nginx/ssl

ADD resources/location.common.conf /etc/nginx
ADD resources/default /etc/nginx/sites-available/default
ADD resources/server.crt /etc/nginx/ssl/server.crt
ADD resources/server.key /etc/nginx/ssl/server.key

CMD ["/usr/bin/supervisord"]
