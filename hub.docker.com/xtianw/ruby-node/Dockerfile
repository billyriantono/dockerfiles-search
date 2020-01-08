FROM ruby:2

RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y sudo

RUN curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash - \
    && sudo apt-get update \
    && sudo apt-get install -y nodejs

RUN gem install bundler --conservative
