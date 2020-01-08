FROM ruby:2.4.4-stretch
MAINTAINER Dongeon Kim <kde713@gmail.com>

RUN apt-get update \
      && apt-get upgrade -y \
      && apt-get install -y locales \
      && echo "en_US UTF-8" > /etc/locale.gen \
      && locale-gen en_US.UTF-8 \
      && export LANG=en_US.UTF-8 \
      && export LANGUAGE=en_US:en \
      && export LC_ALL=en_US.UTF-8 \
      && curl -sL https://deb.nodesource.com/setup_9.x | bash - \
      && apt-get install nodejs -y
