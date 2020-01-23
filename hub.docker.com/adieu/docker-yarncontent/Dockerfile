FROM ruby:2.5-alpine

LABEL Name=achievemore-ruby Version=2.5

WORKDIR /app

RUN gem update bundler

RUN apk --update --upgrade --no-cache add build-base make cmake ninja python git bash curl

RUN apk --update --upgrade --no-cache add mysql-client mysql-dev sqlite-dev zlib-dev libxml2-dev libgcrypt-dev libc6-compat libxslt-dev openssl-dev libressl2.7-libssl tzdata yaml-dev

COPY .bundle/config /usr/local/bundle/

RUN wget https://raw.githubusercontent.com/vishnubob/wait-for-it/master/wait-for-it.sh &&\
    mv wait-for-it.sh /usr/bin &&\
    chmod a+x /usr/bin/wait-for-it.sh

CMD wait-for-it.sh mysql:3306 -- \
    bundle exec rails s -P /app/tmp/pids/backend.pid -p $HTTP_PORT -b 0.0.0.0
