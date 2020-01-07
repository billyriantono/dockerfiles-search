FROM siutin/ubuntu-rvm:v2.3.1_20161018
MAINTAINER Martin Chan <osiutino@gmail.com>
ENV REFRESHED_AT 2017-01-06

USER worker

ENV RAILS_VERSION 5.0.1

RUN /bin/bash -l -c 'gem install rails --version=$RAILS_VERSION --no-doc --no-ri'
