FROM ruby:2.3-alpine

LABEL maintainer="Abed Halawi <abed.halawi@vinelab.com>"

COPY Gemfile Gemfile.lock /usr/src/app/
WORKDIR /usr/src/app

RUN apk add --update nodejs g++ make
RUN bundle install

EXPOSE 4567
CMD ["bundle", "exec", "middleman", "build", "--clean"]
