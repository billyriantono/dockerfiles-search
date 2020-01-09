FROM node:5.2.0-slim
MAINTAINER px3l@tuta.io
RUN \
  curl -sS http://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
  echo "deb http://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
  apt-get update && \
  apt-get install -y yarn && \
  apt-get autoremove -y && \
  apt-get clean all