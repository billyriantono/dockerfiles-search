FROM ruby:2.6.2-alpine

ENV APP_HOME /gameroom-www
ENV BUNDLER_VERSION 2.0.1

RUN apk add --no-cache --update build-base \
                                linux-headers \
                                git \
                                postgresql-dev \
                                tzdata

RUN mkdir $APP_HOME
WORKDIR $APP_HOME

ADD Gemfile* $APP_HOME/
RUN gem update --system
RUN gem install bundler
RUN bundle install

ADD . $APP_HOME

EXPOSE 3000

CMD ["bundle", "exec", "puma", "-t", "5:5"]
