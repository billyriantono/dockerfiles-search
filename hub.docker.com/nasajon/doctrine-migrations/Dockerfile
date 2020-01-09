FROM composer as builder

COPY composer.json /app/

RUN composer install

FROM nasajon/php:7.1-fpm

COPY --from=builder /app/vendor /var/www/html/vendor

WORKDIR /migrations

ENTRYPOINT ["php","/var/www/html/vendor/doctrine/migrations/bin/doctrine-migrations"]
CMD ["migrations:migrate"]
