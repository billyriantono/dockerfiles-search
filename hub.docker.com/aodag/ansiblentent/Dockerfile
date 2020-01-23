FROM ruby:2.6.4-alpine

RUN apk add build-base nodejs yarn sqlite-dev tzdata \
  && rm -rf /var/cache/apk/

RUN gem install rails

WORKDIR /app

EXPOSE 3000

CMD yarn install --check-files && bundle install && rails server -b 0.0.0.0
