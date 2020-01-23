FROM cscadehub/lib-base-backend:latest

COPY ./ /var/www/html

RUN mv /var/www/html/.env.cloud.dev /var/www/html/.env

RUN chmod -R 777 /var/www/html/bootstrap && chmod -R 777 /var/www/html/storage && chmod -R 777 /var/www/html/app/Base

RUN php artisan optimize

RUN php artisan key:generate

#RUN php artisan migrate:refresh

#RUN php artisan db:seed

RUN service apache2 restart

EXPOSE 80
EXPOSE 443