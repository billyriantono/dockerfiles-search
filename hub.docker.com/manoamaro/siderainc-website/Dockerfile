FROM ruby:2.3-alpine

RUN apk update && apk --update add tzdata postgresql-client \
    nodejs sqlite-dev libxml2-dev libxslt-dev git \
    imagemagick

RUN npm install -g bower

ENV RAILS_ENV=production

RUN mkdir -p /app

WORKDIR /app

ADD Gemfile /app
ADD Gemfile.lock /app

RUN apk --update add --virtual build-dependencies build-base ruby-dev openssl-dev \
    postgresql-dev libc-dev linux-headers && \
    gem install bundler && \
    bundle config build.libv8 --with-system-v8 && \
    bundle config build.nokogiri --use-system-libraries && \
    cd /app ; bundle install && \
    apk del build-dependencies

ADD .bowerrc /app
ADD bower.json /app

RUN bower install --allow-root

ADD . /app

RUN bundle exec rake assets:precompile

EXPOSE 3000

CMD bundle exec puma -C config/puma.rb
