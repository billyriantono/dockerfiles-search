FROM node:4

# Set ENV
ENV NODE_ENV dev
ENV npm_config_loglevel error
ENV npm_config_progress false

# Commands
RUN \
  apt-get update && \
  apt-get upgrade -y --force-yes && \
  npm install -g phantomjs-prebuilt@2.1.13 && \
  npm install -g node-sass@3.4.2 && \
  apt-get autoremove -y
