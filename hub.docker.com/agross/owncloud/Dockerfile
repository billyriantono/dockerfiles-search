FROM owncloud:latest

RUN apt-get update && \
    apt-get install --yes --no-install-recommends \
      libmagickwand-dev \
      imagemagick && \
    rm -rf /var/lib/apt/lists/* && \
    \
    pecl install imagick && \
    docker-php-ext-enable imagick
