FROM subosito/ruby:1.9

MAINTAINER Bo Jeanes <me@bjeanes.com>

RUN apt-get install -yq \
      git \
      libqtwebkit-dev \
      postgresql-common libpq-dev \
      openssl gnupg \
      phantomjs

RUN gem install bundler
