FROM php:7.3-fpm-alpine

RUN apk update && \
    apk add --no-cache supervisor

CMD ["supervisord", "-c", "/etc/supervisord.conf"]
