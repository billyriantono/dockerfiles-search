FROM ubuntu AS giter

RUN apt-get update
RUN apt-get install -y git

WORKDIR /git

RUN git clone https://github.com/spiral/roadrunner.git

WORKDIR /git/roadrunner

FROM golang:1.10 AS maker

COPY --from=giter /git /git

WORKDIR /git/roadrunner

RUN go get -d -v ./...

RUN make

FROM composer AS composer

COPY ./app /roadrunner/app

WORKDIR /roadrunner/app

RUN composer require spiral/roadrunner

RUN composer install

FROM php:7.2-cli AS php

WORKDIR /app

COPY --from=composer /roadrunner/app /app

COPY --from=maker /git/roadrunner/rr /app/rr

EXPOSE 8080

ENTRYPOINT [ "./run.sh" ]

