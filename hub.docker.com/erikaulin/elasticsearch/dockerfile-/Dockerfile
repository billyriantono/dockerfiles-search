FROM phpunit/phpunit:4.8.4
MAINTAINER Eric Mann <eric@eamann.com>

RUN apt-get update && \
    apt-get install -y --no-install-recommends libmagickwand-dev && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN pecl install imagick-beta && \
    echo extension=imagick.so > $PHP_INI_DIR/conf.d/ext-imagick.ini

# Set up the application directory.
VOLUME ["/app"]
WORKDIR /app

# Set up the command arguments.
ENTRYPOINT ["/usr/local/bin/phpunit"]
CMD ["--help"]
