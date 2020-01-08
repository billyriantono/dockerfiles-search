FROM ruby:2.2
RUN apt-get update
RUN apt-get dist-upgrade -y
RUN apt-get install curl git-core apache2 nodejs -y
RUN gem update --system
RUN gem install bundler nokogiri rails
RUN mkdir /app
WORKDIR /app 
