FROM ruby:2.3-slim

RUN apt-get update -qq \
# ESSENTIALS
    && apt-get install -y --no-install-recommends curl git imagemagick libmagickwand-dev \
    libgit2-dev docker cmake g++ libicu-dev libmagic-dev inkscape libdb-dev libxml2-dev libxml2-utils \
    libxslt1-dev libgdbm-dev libssl-dev \
# INSTALL NODE
    && curl -sL https://deb.nodesource.com/setup_8.x | bash - \
    && apt-get install -y --no-install-recommends nodejs \
## INSTALL BUNDLER
    && gem install bundler -v '~> 1.17' \
## INSTALL FOREMAN
    && gem install foreman \
## INSTALL YARN
    && curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
    && apt-get install -y --no-install-recommends apt-transport-https \
    && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
    && apt-get update \
    && apt-get install -y --no-install-recommends yarn \
# Clean cache and temp files
    && apt-get clean -qy \
    && rm -rf /var/lib/apt/lists/*
