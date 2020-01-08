### Build stage ###
FROM node:8.14.0

LABEL authors="Samuel Fernandez"

# Install Google Chrome for testing
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -
RUN sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'
RUN apt-get -qq update \
  && apt-get -qq install google-chrome-stable -y --no-install-recommends \
  && apt-get -qq clean \
  && rm -rf /var/lib/apt/lists/*
