FROM ruby:2.4.1
LABEL maintainer="parthmodi54@yahoo.com"

## Install Node.js
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash - && \
    apt-get install -y nodejs && \
    rm -rf /var/lib/apt/lists/*
    
# throw errors if Gemfile has been modified since Gemfile.lock
RUN bundle config --global frozen 1