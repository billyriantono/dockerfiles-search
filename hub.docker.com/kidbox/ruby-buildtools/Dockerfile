FROM ruby:2.3.2-slim

MAINTAINER Kobi Meirson <kobi@kidbox.com>

RUN apt-get update -qq && apt-get install -y build-essential

# for nokogiri
RUN apt-get install -y libxml2-dev libxslt1-dev
