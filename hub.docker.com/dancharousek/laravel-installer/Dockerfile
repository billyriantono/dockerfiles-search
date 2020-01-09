FROM php:7.2-cli-alpine

COPY . /usr/src/app
WORKDIR /usr/src/app

RUN chmod +x scripts/* && \
    ./scripts/init_scripts.sh

ENTRYPOINT ["php", "application.php"]
