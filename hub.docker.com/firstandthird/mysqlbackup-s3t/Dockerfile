FROM ruby:2.5.1-stretch

ENV RAILS_VERSION=5.2.0
ENV NODEJS_VERSION=4.8.2~dfsg-1

# Update package cache
RUN apt-get update

# Install Node JS
RUN apt-get install -y nodejs=$NODEJS_VERSION

# Install Rails
RUN gem install rails -v $RAILS_VERSION

# Force installation of dependencies
RUN \
  cd /tmp && \
  rails new throwaway && \
  rm -Rf /tmp/throwaway
