FROM ruby:2.6.3-slim

ENV APP_HOME="/odonto_clean"
ENV BUNDLE_PATH="$GEM_HOME" HISTFILE="$APP_HOME/tmp/docker_histfile"

# Config for the terminal
COPY .bashrc /root/.bashrc

RUN apt-get update -y \
  && apt-get install -y --no-install-recommends gnupg wget \
  && wget -q -O - https://deb.nodesource.com/setup_12.x | bash - \
  && mkdir -p /usr/share/man/man1 \
  && mkdir -p /usr/share/man/man7 \
  && apt-get install -y --no-install-recommends \
                        make gcc g++ libpq-dev nodejs \
                        postgresql-client git \
                        libsqlite3-dev \
  && npm install -g yarn \
  && rm -rf /var/lib/apt/lists/* /tmp/* \
  && apt-get autoremove \
  && apt-get autoclean

# Cache the bundle install gems
COPY Gemfile* /cached-gems/
WORKDIR /cached-gems
RUN bundle check || (bundle install --no-cache --jobs=2 \
      && bundle clean --force \
      && rm -rf "$BUNDLE_PATH/gems/*/.git" \
      && rm -rf "$BUNDLE_PATH/bundler/gems/*/.git")

# Cache yarn install
COPY package.json yarn.lock /$APP_HOME/
WORKDIR $APP_HOME
RUN yarn install && yarn cache clean

COPY . .

RUN rm -rf log/*

EXPOSE 3000

CMD sh ./scripts/start.sh
