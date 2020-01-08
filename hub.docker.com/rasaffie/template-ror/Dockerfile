FROM ruby:2.3.1

RUN apt-get update -qq
RUN apt-get install -y build-essential libpq-dev nodejs npm

RUN gem uninstall -i /usr/local/lib/ruby/gems/2.3.0 bundler
RUN gem uninstall -i /usr/local/lib/ruby/gems/2.3.0 rake
RUN gem install bundler --version '1.11.2'

RUN npm install -g jshint@2.9.3
RUN npm install -g csslint@1.0.3
RUN npm install -g jscs@3.0.7;

RUN ln -s /usr/bin/nodejs /usr/bin/node

ENV APP_HOME /template-ror
ENV RAILS_ENV development

RUN mkdir $APP_HOME
WORKDIR $APP_HOME

ADD Gemfile $APP_HOME/Gemfile
ADD Gemfile.lock  $APP_HOME/Gemfile.lock
RUN bundle install --jobs=3 --retry=3 --without=production

ADD . $APP_HOME
