# vim:set ft=dockerfile:
FROM node:6

ENV RUBY_DOWNLOAD_SHA256 ba5ba60e5f1aa21b4ef8e9bf35b9ddb57286cb546aac4b5a28c71f459467e507
ADD https://cache.ruby-lang.org/pub/ruby/2.3/ruby-2.3.0.tar.gz /tmp/

# Install ruby
RUN \
  cd /tmp && \
  echo "$RUBY_DOWNLOAD_SHA256 *ruby-2.3.0.tar.gz" | sha256sum -c - && \
  tar -xzf ruby-2.3.0.tar.gz && \
  cd ruby-2.3.0 && \
  ./configure && \
  make && \
  make install && \
  cd .. && \
  rm -rf ruby-2.3.0 && \
  rm -f ruby-2.3.0.tar.gz

RUN gem install bundler --no-ri --no-rdoc
RUN gem install jekyll