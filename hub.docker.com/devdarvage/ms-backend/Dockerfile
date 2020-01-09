FROM devdarvage/ms-base-backend:latest

COPY ./docker/supervisord.conf /etc/supervisor/conf.d/supervisord.conf

RUN mkdir -p /var/log/supervisor

COPY ./ /var/www/html

RUN mv /var/www/html/.env.build.dev /var/www/html/.env

RUN chmod -R 777 /var/www/html/bootstrap && chmod -R 777 /var/www/html/storage

VOLUME ["/var/www/html/vendor", "/var/www/html/node_modules", "/var/www/html/public/bower_components", "/var/www/html/public/compiled"]

EXPOSE 80
EXPOSE 443

CMD ["/usr/bin/supervisord"]