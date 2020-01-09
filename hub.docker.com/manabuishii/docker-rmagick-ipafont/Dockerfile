FROM ruby:2.2.4
RUN gem install rmagick -v 2.15.4
RUN apt-get update; apt-get install -y imagemagick fonts-ipafont ; apt-get clean
ADD sample.rb /usr/local/bin/
