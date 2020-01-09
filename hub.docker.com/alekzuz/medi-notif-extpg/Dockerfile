########################

FROM ruby:2.6.3
 
RUN mkdir /notif_ms
WORKDIR /notif_ms
 
ADD Gemfile /notif_ms/Gemfile
ADD Gemfile.lock /notif_ms/Gemfile.lock

RUN apt-get update -qq && apt-get install -y nodejs postgresql-client
RUN gem install bundler

# RUN bundle update --bundler
RUN gem install bundler --pre

RUN bundle install --binstubs    
RUN bundle binstubs bundler --force

RUN bundle install


ADD . /notif_ms
 
EXPOSE 5004
