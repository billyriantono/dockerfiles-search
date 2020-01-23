FROM adie/debian

MAINTAINER Anton Dieterle <antondie@gmail.com>

# Ruby-related packages
RUN apt-get update -qq \
    && apt-get install -y \
      autoconf \
      build-essential \
      libcurl4-openssl-dev \
      libffi-dev \
      libgdbm-dev \
      libncurses5-dev \
      libreadline-dev \
      libssl-dev \
      libyaml-dev \
      zlib1g-dev \
    && rm -rf /var/lib/apt/lists/*

ENV RUBY_VERSION 2.3.1

# Install ruby and bundler
RUN cd /tmp \
    && wget -O ruby-install-0.6.0.tar.gz https://github.com/postmodern/ruby-install/archive/v0.6.0.tar.gz \
    && tar -xzvf ruby-install-0.6.0.tar.gz \
    && ruby-install-0.6.0/bin/ruby-install --system --cleanup --no-install-deps -j9 ruby $RUBY_VERSION -- --disable-install-doc \
    && rm -rf /tmp/* \
    && echo "gem: --no-document" >> /usr/local/etc/gemrc \
    && gem install bundler
