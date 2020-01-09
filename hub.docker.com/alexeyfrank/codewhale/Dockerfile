FROM ruby:2.1.3

# throw errors if Gemfile has been modified since Gemfile.lock
RUN bundle config --global frozen 1

RUN apt-get update -qq && apt-get install -y build-essential libpq-dev libxml2 nodejs npm
RUN ln -s /usr/bin/nodejs /usr/bin/node

RUN npm i -g gulp

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

ADD package.json /usr/src/app/
RUN npm i

ADD Gemfile /usr/src/app/
ADD Gemfile.lock /usr/src/app/
RUN bundle install

ADD ./config/database.sample.yml /usr/src/app/config/database.yml
ADD . /usr/src/app

RUN gulp assets_precompile
RUN RAILS_ENV=production ./bin/rake assets:precompile

CMD ["puma", "-C", "config/puma.rb"]
# CMD ["./bin/rails", "s"]
