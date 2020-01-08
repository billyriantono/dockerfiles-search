FROM ubuntu:16.04
MAINTAINER Toshimitsu Takahashi <toshi@tilfin.com>

RUN apt-get update
RUN apt-get install -y --no-install-recommends \
     curl git nodejs nodejs-legacy npm firefox chromium-browser \
     phantomjs xvfb && \
  apt-get autoremove -y --purge && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN npm install -g bower gulp jasmine-core webpack \
  jasmine-node jasmine-reporters \
  karma karma-jasmine karma-webpack \
  karma-chrome-launcher \
  karma-firefox-launcher

ENV NODE_PATH /usr/lib/nodejs/:/usr/local/lib/node_modules/

ENTRYPOINT []
