FROM rails:latest
MAINTAINER Roberto Nogueira <enogrob@gmail.com>

# Deploy Rails App.
WORKDIR /usr/src/app
ADD Gemfile* ./
RUN gem install bundler && bundle install
COPY . ./
