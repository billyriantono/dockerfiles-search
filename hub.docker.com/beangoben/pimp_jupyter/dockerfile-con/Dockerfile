FROM debian:wheezy

RUN apt-get update && apt-get install -y \
  build-essential \
  libncurses-dev \
  libreadline-dev \
  zlib1g-dev \
  libssl-dev \
  libsqlite3-dev

ADD ruby-2.1.2p95_amd64.deb /tmp/ruby-2.1.2p95_amd64.deb
RUN dpkg -i /tmp/ruby-2.1.2p95_amd64.deb

ADD Gemfile /tmp/Gemfile
RUN echo 'gem: --no-rdoc --no-ri' >> /.gemrc
RUN gem install bundler
RUN bundle install --gemfile=/tmp/Gemfile
