FROM 4armed/ruby:2.3.4
MAINTAINER Marc Wickenden <marc@4armed.com>

RUN apt-get update && apt-get install -y build-essential zip libmysqlclient-dev libpq-dev libaio1 imagemagick libmagickwand-dev && rm -rf /var/lib/apt/lists/*

RUN echo 'gem: --no-rdoc --no-ri' >> $HOME/.gemrc && \
    gem install bundler && \
    bundle config path /remote_gems

WORKDIR /app
ONBUILD ADD Gemfile /app/Gemfile
ONBUILD ADD Gemfile.lock /app/Gemfile.lock
ONBUILD ADD . /app
ONBUILD RUN bundle install --deployment --without development test
ONBUILD RUN bundle exec rake assets:precompile

ENV RAILS_ENV production
ENV RACK_ENV production

EXPOSE 8080

CMD bundle exec unicorn -c config/unicorn.rb
