FROM ruby:2.5
LABEL maintainer="Akira Koyasu <mail@akirakoyasu.net>"

COPY /Gemfile /srv/jekyll/Gemfile
WORKDIR /srv/jekyll
RUN bundle install
