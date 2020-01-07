FROM ruby:2.4.3

ENV LANG ja_JP.UTF-8

RUN curl -sL https://deb.nodesource.com/setup_9.x | bash -
RUN apt-get update -qq && apt-get install -y \
    build-essential \
    git \
    curl \
    libcurl4-openssl-dev \
    zlib1g-dev \
    libssl-dev \
    libreadline-dev \
    libxml2-dev \
    libxslt-dev \
    libyaml-dev \
    mysql-client \
    libmysqlclient-dev \
    strace \
    nodejs \
    tzdata

ENV ENTRYKIT_VERSION 0.4.0
# EntryKitのインストール
RUN wget https://github.com/progrium/entrykit/releases/download/v${ENTRYKIT_VERSION}/entrykit_${ENTRYKIT_VERSION}_Linux_x86_64.tgz \
  && tar -xvzf entrykit_${ENTRYKIT_VERSION}_Linux_x86_64.tgz \
  && rm entrykit_${ENTRYKIT_VERSION}_Linux_x86_64.tgz \
  && mv entrykit /bin/entrykit \
  && chmod +x /bin/entrykit \
  && entrykit --symlink

RUN mkdir /app

WORKDIR /app
COPY Gemfile Gemfile.lock /app/
RUN bash -l -c 'bundle install --no-cache --deployment --jobs 4 --without development test'
COPY . /app
ENV RAILS_ENV production

EXPOSE 3000

# Use EntryKit
ENTRYPOINT [ \
  "prehook", "ruby -v", "--", \
  "switch", \
    "shell=/bin/sh", \
    "rails_c=bundle exec rails c", \
    "rails_s=bundle exec rails s -b 0.0.0.0", "--", \
  "bundle", "exec", "unicorn_rails", "-c", "config/unicorn.rb" ]
