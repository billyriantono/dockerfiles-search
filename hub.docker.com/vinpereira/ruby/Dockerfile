FROM vinpereira/rbenv
MAINTAINER Vinícius Pereira <vp.vinicius.pereira@gmail.com>

ENV RUBY_VERSION 2.4.1

RUN apt-get update -q \
  && apt-get -q -y install autoconf bison build-essential libssl-dev libyaml-dev libreadline6-dev zlib1g-dev \
  && rbenv install $RUBY_VERSION \
  && rbenv global $RUBY_VERSION \
  && apt-get purge -y -q autoconf bison build-essential libssl-dev zlib1g-dev \
  && apt-get autoremove -y \
  && rm -rf /var/lib/apt/lists

RUN gem install --no-ri --no-rdoc bundler
RUN rbenv rehash
