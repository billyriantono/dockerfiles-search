# Inspired by official ruby images.
#
# Could be used as base image for development.
#
# For production purpose create another image with only one
# 'RUN' including rails, sinatra, ... and 'apt-get autoremove --purge'
# to have an image as small as possible. See comments below.

FROM debian:jessie
MAINTAINER Samuel GAY "sam.onzeweb@gmail.com"

ENV RUBY_MAJOR 2.3
ENV RUBY_VERSION 2.3.1

ENV GEM_HOME /usr/local/bundle
ENV PATH $GEM_HOME/bin:$PATH
ENV BUNDLE_APP_CONFIG $GEM_HOME

ENV REFRESHED_AT 2016-06-04

RUN apt-get -qq update \
    && apt-get -y install build-essential \
                          git \
                          curl \
                          zlib1g-dev \
                          libreadline-dev \
                          libssl-dev \
                          libffi-dev \
    && mkdir -p /usr/src/ruby \
    && curl -SL "http://cache.ruby-lang.org/pub/ruby/$RUBY_MAJOR/ruby-$RUBY_VERSION.tar.bz2" \
       | tar -xjC /usr/src/ruby --strip-components=1 \
    && cd /usr/src/ruby \
    && ./configure --disable-install-doc \
    && make -j"$(nproc)" \
    && make install \
    && cd $HOME \
    && rm -r /usr/src/ruby\
    && echo 'gem: --no-rdoc --no-ri' >> "$HOME/.gemrc" \
    && gem install bundler \
    && bundle config --global path "$GEM_HOME" \
    && bundle config --global bin "$GEM_HOME/bin"
# For production use add some things here within the same RUN command
#   && <-- here
# and remove as much things as possible to have a small images
#    && apt-get autoremove --purge build-essential \
#                                  git \
#                                  curl \
#                                  zlib1g-dev \
#                                  libreadline-dev \
#                                  libssl-dev \
#                                  libffi-dev

CMD ["/bin/bash"]
