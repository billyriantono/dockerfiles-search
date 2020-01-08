FROM ubuntu:14.04

MAINTAINER Tom Rudick <tmrudick@gmail.com>

# Update packages and install builds tools
RUN apt-get update && \
    apt-get install -y git-core build-essential curl libffi-dev libgdbm-dev libncurses5-dev libreadline-dev libssl-dev libyaml-dev zlib1g-dev libpq-dev && \
    apt-get clean && \
    rm -rf /var/lib/apt

# Build Ruby
WORKDIR /root
RUN curl http://cache.ruby-lang.org/pub/ruby/2.1/ruby-2.1.2.tar.gz  | tar -xzvf - && \
  cd /root/ruby-2.1.2 && \
  ./configure && \
  make && \
  make install && \
  cd / && \
  rm -rf /root/ruby-2.1.2

# Install bundler
RUN echo "gem: --no-ri --no-rdoc" > ~/.gemrc
RUN gem install bundler
