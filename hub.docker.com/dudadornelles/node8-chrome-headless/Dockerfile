FROM node:8-slim

RUN wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb && \
  apt-get update && \
  apt-get install -y \
  fonts-liberation \
  libappindicator3-1 \
  libasound2 \
  libatk-bridge2.0-0 \
  libatk1.0-0 \
  libcairo2 \
  libcups2 \
  libdbus-1-3 \
  libexpat1 \
  libnspr4 \
  libnss3 \
  libx11-xcb1 \
  libxss1 \
  lsb-release  \
  xdg-utils \
  openjdk-7-jdk && \
  dpkg -i google-chrome-stable_current_amd64.deb && \
  rm -rf /var/lib/apt/lists/* /var/apt/cache/* /tmp/*
