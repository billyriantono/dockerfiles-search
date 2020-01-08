FROM ruby:2.4.2
MAINTAINER Omar Johnson

# Install nodejs
RUN curl -sL https://deb.nodesource.com/setup_7.x | bash -

# Install yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

# Install packages
RUN apt-get update -qq && \
    apt-get install -y \
        build-essential \
        libpq-dev \
        nodejs \
        yarn \
        qt5-default \
        libqt5webkit5-dev \
        gstreamer1.0-plugins-base \
        gstreamer1.0-tools \
        gstreamer1.0-x \
        postgresql \
        postgresql-client-common \
        postgresql-contrib && \
    rm -rf /var/lib/apt/lists/*

# Setup directory
RUN mkdir -p /app
WORKDIR /app

# Install Gems
ADD Gemfile Gemfile.lock ./
ENV BUNDLE_JOBS=8 BUNDLE_PATH=/bundle
RUN bundle install

ADD . .
