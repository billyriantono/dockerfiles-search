FROM ubuntu:16.04

# Update and install basic packages
RUN  apt-get update \
  && apt-get install -y wget \
  build-essential \
  ca-certificates \
  gcc \
  apt-transport-https \
  && rm -rf /var/lib/apt/lists/*

# Install deps + add Chrome Stable + purge all the things
RUN wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | apt-key add - \
  && echo "deb https://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list \
  && apt-get update -qqy \
  && apt-get -qqy install google-chrome-unstable \
  && rm /etc/apt/sources.list.d/google-chrome.list \
  && rm -rf /var/lib/apt/lists/* /var/cache/apt/*
