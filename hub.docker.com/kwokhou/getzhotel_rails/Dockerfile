# Base image from Ruby docker hub
FROM ruby:2.3.1

# Install essential linux packages
RUN apt-get update -qq && apt-get install -y --no-install-recommends \
    build-essential \
    libpq-dev \
    nodejs \
    npm \
    postgresql-client \
    && rm -rf /var/lib/apt/lists/*

# Define where the application will live inside the image
ENV RAILS_ROOT /var/www/app

# Create application home. App server will need the pids dir
RUN mkdir -p $RAILS_ROOT/tmp/pids

# Set our working directory inside the image
WORKDIR $RAILS_ROOT

# Copy NPM package config
COPY package.json package.json

# Restore npm packages
RUN NODE_ENV=production npm install

# Prevent bundler warnings; Ensure bundler version is >= that which created Gemfile.lock
RUN gem install bundler

# Use the Gemfiles as Docker cache markers. Always bundle before copying app src.
# (the src likely changed and we don't want to invalidate Docker's cache too early)
# http://ilikestuffblog.com/2014/01/06/how-to-skip-bundle-install-when-deploying-a-rails-app-to-docker/

COPY Gemfile Gemfile

COPY Gemfile.lock Gemfile.lock

# Finish establishing our Ruby enviornment
RUN bundle install --deployment

