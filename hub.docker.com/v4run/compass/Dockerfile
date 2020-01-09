#################################################################################################
# Dockerfile to build container images with nodejs, compass and bootstrap-sass
#################################################################################################

FROM node:latest

MAINTAINER Varun Vasan V

# Updating image
RUN apt-get update

# Installing ruby and bundle
RUN apt-get install -y ruby-full && gem install bundle

COPY Gemfile /var/tmp/Gemfile

WORKDIR /var/tmp/

# Installing gems in Gemfile
RUN bundle install

RUN mkdir /config

WORKDIR /config