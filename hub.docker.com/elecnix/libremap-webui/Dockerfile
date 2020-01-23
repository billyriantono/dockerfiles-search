FROM debian:jessie

MAINTAINER Nicolas Marchildon nicolas@marchildon.net

ENV DEBIAN_FRONTEND noninteractive

# Install NodeJS, NPM, Grunt
# https://github.com/joyent/node/wiki/installing-node.js-via-package-manager
RUN apt-get update && \
  apt-get install -y curl git && \
  curl -sL https://deb.nodesource.com/setup | bash - && \
  apt-get install -y nodejs && \
  npm install -g grunt-cli bower

RUN useradd -m libremap
WORKDIR /home/libremap
COPY . /home/libremap/webui
WORKDIR /home/libremap/webui
RUN chown -R libremap: .
USER libremap
RUN npm install
RUN bower install
RUN cp config.json.example config.json && \
  sed -i -e 's#"api_url": ".*"#"api_url": "http://localhost:5484/api"#' config.json

ENTRYPOINT exec grunt
EXPOSE 9000

