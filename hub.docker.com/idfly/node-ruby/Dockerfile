FROM node

ENV PATH=$PATH:/app/node_modules/.bin:/app/vendor/bundle/ruby/2.1.0/bin
ENV GEM_PATH=/var/lib/gems/2.1.0:/root/.gem/ruby/2.1.0:/app/vendor/bundle/ruby/2.1.0

WORKDIR /app

RUN apt-get update
RUN apt-get install -y \
  ruby \
  ruby-dev

RUN gem install --no-ri --no-rdoc \
  bundler
