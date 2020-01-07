FROM golang

WORKDIR /app

RUN apt-get update && apt-get install -y \
  ruby \
  ruby-dev

RUN gem install --no-ri --no-rdoc \
  bundler

RUN mkdir /usr/local/bundle
RUN echo "---\nBUNDLE_PATH: .build/vendor/bundle" > /usr/local/bundle/config

ENV GOPATH=/go
ENV PATH=/go/bin:/usr/local/go/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/app/.build/vendor/bundle/ruby/2.1.0/bin
ENV GEM_PATH=/var/lib/gems/2.1.0:/root/.gem/ruby/2.1.0:/app/.build/vendor/bundle/ruby/2.1.0
