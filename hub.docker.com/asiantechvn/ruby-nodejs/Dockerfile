FROM ruby:2.5

ENV LANG C.UTF-8 \
  BUNDLE_BIN /usr/local/bundle/bin \
  DOCKER 1

RUN apt-get update \
  && apt-get install -y --no-install-recommends qt5-default libqt5webkit5-dev gstreamer1.0-plugins-base gstreamer1.0-tools gstreamer1.0-x xvfb imagemagick \
  && apt-get install -y nodejs postgresql-client
