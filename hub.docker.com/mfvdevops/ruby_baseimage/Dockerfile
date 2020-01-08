#-----------------------------------------#
# Common to development/staging/production
#-----------------------------------------#
FROM ruby:2.6.5-alpine

### Install dependent packages
RUN apk --update --upgrade add --virtual deps \
      gcc g++ make \
      python3-dev linux-headers musl-dev \
      git jq curl build-base mysql-dev tzdata nodejs \
      alpine-sdk gmp-dev libffi-dev \
      postgresql-dev && \
    apk --update --upgrade add --no-cache libpq gmp && \
    cp -p /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

RUN apk add --update busybox-suid

ENV APP_DIR /app

RUN mkdir -p $APP_DIR

WORKDIR $APP_DIR
