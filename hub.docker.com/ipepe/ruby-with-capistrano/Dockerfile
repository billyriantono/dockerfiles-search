FROM ruby:2.3.1
MAINTAINER docker@ipepe.pl

ADD Gemfile .
RUN bundle install && rm Gemfile*
