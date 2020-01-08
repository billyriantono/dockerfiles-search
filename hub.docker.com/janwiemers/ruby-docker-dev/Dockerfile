FROM ruby:2.6.1-alpine3.9

RUN apk add --update build-base \
        postgresql-dev \
        nodejs-current \
        imagemagick \
        tzdata \
        python \
        yarn \
        git

RUN gem install bundler

WORKDIR /app
