FROM ruby:2.5.3-alpine3.8

RUN apk add --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/main && \
    apk update && apk upgrade && \
    apk add build-base bash dcron && \
    apk upgrade --available && \
    rm -rf /var/cache/apk/* && \
    mkdir /usr/app

WORKDIR /usr/app

COPY Gemfile* /usr/app/

RUN bundle install

COPY . /usr/app

RUN bundle exec whenever -c && bundle exec whenever --update-crontab && mkdir ./log && touch ./log/cron.log

ENTRYPOINT crond && tail -f ./log/cron.log
