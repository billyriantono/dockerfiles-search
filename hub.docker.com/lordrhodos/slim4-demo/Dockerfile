FROM lordrhodos/slim-docker:latest

ENV COMPOSER_ALLOW_SUPERUSER=1

COPY . /var/www/app

RUN composer install

RUN rm .gitignore -Rf composer.json composer.lock docker-compose.yml Dockerfile apache.conf README.md
