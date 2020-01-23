# rails-dev in a container
#
# There are many images like it, but this one is mine. You probably don't want
# to use this.
#
# ```bash
# docker run \
#   --rm \
#   --it \
#   -v .:/app \
#   andrewsardone/docker-rails-dev
# ```
#
# You should make a Dockerfile for your own app that inherits from this guy and
# copies in your Gemfile and bundle installs:
#
# ```
# COPY Gemfile /app/Gemfile
# COPY Gemfile.lock /app/Gemfile.lock
#
# RUN bundle install
#
# COPY . /app
# ```

FROM ruby:2.5
MAINTAINER Andrew Sardone <andrew@andrewsardone.com>
LABEL description="An Andrew Rails development environment within a container"

RUN curl --silent --location https://deb.nodesource.com/setup_8.x | bash - && \
  curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
  echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
  apt-get update -qqy && \
  apt-get install -y \
    build-essential \
    libpq-dev \
    nodejs \
    yarn && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN mkdir /app
WORKDIR /app

CMD [ "bash" ]
