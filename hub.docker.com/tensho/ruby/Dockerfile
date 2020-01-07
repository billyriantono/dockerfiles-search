# FROM scratch
# FROM debian:jessie
# FROM buildpack-deps:jessie
FROM tensho/rbenv
MAINTAINER Andrew Babichev <andrew.babichev@gmail.com>

ENV RUBY_VERSION 2.2.3

# Install ruby
RUN rbenv install $RUBY_VERSION
RUN rbenv global $RUBY_VERSION

# Disable gems documentation generation
RUN echo 'gem: --no-document' >> "/.gemrc"

# Install bundler
RUN gem install bundler

CMD [ "irb" ]
