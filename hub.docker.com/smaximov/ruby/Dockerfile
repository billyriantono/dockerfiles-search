FROM ruby:2.5.1
MAINTAINER smaximov <s.b.maximov@gmail.com>

ARG APT_KEY_DONT_WARN_ON_DANGEROUS_USAGE=1

# Add chrome repository
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - && \
    sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list'

# Install dependencies
RUN apt-get update -qq && apt-get install -y -qq \
      google-chrome-stable \
      gstreamer1.0-plugins-base \
      gstreamer1.0-tools \
      gstreamer1.0-x \
      libnss3-dev \
      nodejs \
      unzip \
      xvfb

# Install chromedriver
RUN export CHROMEDRIVER_RELEASE=$(curl --location --fail --retry 3 http://chromedriver.storage.googleapis.com/LATEST_RELEASE_73) && \
     curl --silent --show-error --location --fail --retry 3 --output /tmp/chromedriver_linux64.zip "http://chromedriver.storage.googleapis.com/$CHROMEDRIVER_RELEASE/chromedriver_linux64.zip" && \
     cd /tmp && \
     unzip chromedriver_linux64.zip && \
     rm -rf chromedriver_linux64.zip && \
     install chromedriver --mode 755 /usr/local/bin/chromedriver && \
     rm chromedriver

# Install libsodium
ARG LIBSODIUM_VERSION=1.0.17

RUN cd /tmp && \
     wget https://download.libsodium.org/libsodium/releases/libsodium-${LIBSODIUM_VERSION}.tar.gz && \
     tar xzf libsodium-${LIBSODIUM_VERSION}.tar.gz && \
     cd libsodium-${LIBSODIUM_VERSION} && \
     ./configure && \
     make && \
     make check && \
     rm -rf /tmp/libsodium-*
