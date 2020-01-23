FROM ruby:2.3.8

# Install the dependencies
RUN apt-get update && \
  apt-get -y install \
    nodejs \
    qt5-default \
    libqt5webkit5-dev \
    gstreamer1.0-plugins-base \
    gstreamer1.0-tools \
    gstreamer1.0-x && \
  rm -rf /var/lib/apt/lists/*
