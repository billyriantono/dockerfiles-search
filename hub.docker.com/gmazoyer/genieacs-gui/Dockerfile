FROM ruby:2-slim

RUN apt-get update \
    && apt-get install -y wget gnupg git libsqlite3-dev build-essential \
    && wget -O - https://deb.nodesource.com/setup_6.x | bash \
    && apt-get install -y nodejs

RUN mkdir /app \
    && cd /app \
    && git clone https://github.com/zaidka/genieacs-gui.git .

WORKDIR /app
RUN bundle install

ENTRYPOINT ["/app/bin/rails", "s", "-b", "0.0.0.0", "-p", "80"]
