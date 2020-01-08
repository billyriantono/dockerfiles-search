FROM composer/composer:1-alpine
RUN apk update; apk add openssh-client
COPY ./src/ /usr/local/
ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
