FROM alpine:3.9

LABEL maintainer="anniluenchen@googlemail.com"

RUN apk add --no-cache \
        composer \
        php7

WORKDIR /datechecker

ADD . /datechecker

RUN composer install --no-dev

CMD php artisan get:salaryFile --filename=salary.csv && cat storage/salary.csv
