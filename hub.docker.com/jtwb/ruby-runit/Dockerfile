# See https://github.com/phusion/baseimage-docker/blob/master/Changelog.md
FROM phusion/baseimage:0.9.9

# Inspired by https://github.com/lgs/docker-ruby-2.1.1p76

ADD http://cache.ruby-lang.org/pub/ruby/2.0/ruby-2.0.0-p451.tar.gz / 

# Change REFRESHED_AT date to force local image update
ENV REFRESHED_AT 2014-15-03

RUN apt-get -qq update && apt-get install -y tar git build-essential \
    zlib1g-dev libssl-dev libreadline6-dev libyaml-dev && tar -xzf ruby-2.0.0-p451.tar.gz && \
    (cd ruby-2.0.0-p451/ && ./configure --disable-install-doc && make && make install) && \
    rm -rf /ruby-2.0.0-p451* && gem install bundler --no-rdoc --no-ri && apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

