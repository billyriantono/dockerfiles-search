FROM navidonskis/nginx-php5.6

WORKDIR /var/www

COPY composer*.json ./
RUN composer install

COPY . .

EXPOSE 80