FROM ubuntu:16.04
MAINTAINER panage

EXPOSE 2400

RUN apt-get update
RUN apt-get install -y --no-install-recommends \
  ansible \
  nodejs-legacy \
  npm

RUN npm install ansibrest -g

WORKDIR /usr/local/lib/node_modules/ansibrest
CMD ansibrest
