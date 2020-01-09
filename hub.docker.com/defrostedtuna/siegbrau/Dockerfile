FROM learninghouse/nginx-phpfpm:7.2

RUN apk --no-cache add \
    php7-fileinfo \
    php7-xml \
    php7-xmlwriter

COPY . /app

RUN composer install --no-dev --no-suggest --optimize-autoloader && \
    rm -rf /root/.composer

RUN chown -R www:www /app
RUN chmod -R ug+rwx /app/storage /app/bootstrap/cache
RUN chmod -R 777 /app/storage/logs