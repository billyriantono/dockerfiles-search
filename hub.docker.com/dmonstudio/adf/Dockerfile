FROM node:alpine AS static

WORKDIR /build

RUN apk add --no-cache python2 build-base
RUN mkdir /build/public

COPY src/package.json /build/
RUN npm i

COPY src/resources /build/resources
COPY src/artisan /build/
COPY src/webpack.mix.js /build/

RUN npm run prod

FROM composer AS deps

WORKDIR /build

COPY src/composer.json /build/
COPY src/composer.lock /build/

RUN composer install --no-dev -o --ignore-platform-reqs --no-scripts

FROM sudomabider/php7-nginx

RUN apk add --no-cache postgresql-dev && \
    docker-php-ext-install pdo pdo_pgsql

COPY nginx.conf /etc/nginx/conf.d/default.conf
COPY --chown=www-data:www-data --from=static /build/public/ /app/public/
COPY --chown=www-data:www-data --from=deps /build/vendor /app/vendor
COPY --chown=www-data:www-data src /app

RUN php artisan package:discover
