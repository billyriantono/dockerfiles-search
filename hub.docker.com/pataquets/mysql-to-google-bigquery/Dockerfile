FROM composer/composer

COPY ./composer.json ./composer.lock /usr/src/app/
WORKDIR /usr/src/app/

RUN \
  composer install --verbose && \
  composer clear-cache && \
  rm -rf ~/.composer/cache

COPY . /usr/src/app/

ENTRYPOINT [ "bin/console" ]
