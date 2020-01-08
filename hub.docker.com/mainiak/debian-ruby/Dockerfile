FROM debian:wheezy
VOLUME /app
RUN apt-get update && apt-get upgrade -y && \
  apt-get install -y ruby vim-nox && \
  gem install bundler
