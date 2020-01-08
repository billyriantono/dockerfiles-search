FROM ruby:2.5.1
MAINTAINER Way Man K "khcjump@gmail.com"

#reference https://hub.docker.com/_/ruby/

ENV RUBY_VERSION 2.5.1
ENV RAILS_VERSION 5.0.2
ENV NODEJS_VERSION 8.11.3
ENV MARIADB_CLIENT_VERSION 10.1

RUN apt-get update ;\
    apt-get install -y nodejs ;\
    apt-get install -y mariadb-client

RUN bundle config --global frozen 1 ;\
    gem install rails -v ${RAILS_VERSION}

COPY ./app/ /app
WORKDIR /app
RUN bundle install
EXPOSE 3000
CMD ["rails","server"]
