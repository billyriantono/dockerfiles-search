FROM ruby:2.5.3-slim

ENV DEBIAN_FRONTEND noninteractive

# Enable parallel downloads in apt
RUN echo 'Acquire::Queue-Mode "host";' >> /etc/apt/apt.conf # Change host for access to disable parallel downloads

# Force apt to retry downloads
RUN echo 'APT::Acquire::Retries=10;' >> /etc/apt/apt.conf

RUN apt-get update && apt-get install -y \
  curl \
  git-core \
  build-essential \
  patch \
  sqlite3 \
  libxslt1-dev \
  liblzma-dev \
  locales

RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8
RUN dpkg-reconfigure locales

ENV APP_HOME /usr/src/app
RUN mkdir -p $APP_HOME
WORKDIR $APP_HOME
ADD Gemfile* $APP_HOME/
RUN bundle install --jobs=4 --retry=3

ADD . $APP_HOME
