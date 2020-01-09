FROM ubuntu:precise
MAINTAINER Lewis Marshall <lewis@lmars.net>

# Update sources
RUN apt-get update

# Install Ruby dependencies
RUN apt-get install -y build-essential libyaml-dev libffi-dev \
    libreadline6-dev libssl-dev libyaml-dev zlib1g-dev

# Install wget and ca-certificates so can download source files via SSL
RUN apt-get install -y wget ca-certificates

# Install ruby-build
ENV RUBY_BUILD_URL https://github.com/sstephenson/ruby-build/archive/v20131225.1.tar.gz
RUN mkdir -p /usr/local/ruby-build && \
    wget -O - $RUBY_BUILD_URL | tar xzf - --strip-components=1 -C /usr/local/ruby-build

# Install Ruby 2.0.0-p353
RUN /usr/local/ruby-build/bin/ruby-build 2.0.0-p353 /usr/local

# Install Bundler
RUN gem install bundler --no-ri --no-rdoc