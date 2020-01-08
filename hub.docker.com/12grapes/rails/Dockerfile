# Base our image on an official, minimal image of our preferred Ruby
FROM ruby:2.3.1-slim

RUN \
  echo "deb http://www.deb-multimedia.org jessie main non-free" >> /etc/apt/sources.list && \
  echo "deb-src http://www.deb-multimedia.org jessie main non-free" >> /etc/apt/sources.list

# Install build dependencies
RUN \
  apt-get update && apt-get install -y --force-yes \
  build-essential \
  nodejs \
  libsqlite3-dev \
  libmysqlclient-dev \
  git \
  imagemagick \
  vim \
  ntp \
  libxml2-dev \
  libxslt-dev \
  file \
  deb-multimedia-keyring && \
  apt-get update -qq && \
  apt-get dist-upgrade -y && \
  apt-get install -y ffmpeg
  # ffmpeg installation based on
  # https://www.assetbank.co.uk/support/documentation/install/ffmpeg-debian-squeeze/ffmpeg-debian-jessie/

RUN gem install bundler
