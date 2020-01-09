FROM ubuntu
MAINTAINER Digital Maelstrom <info@digitalmaelstrom.net>
RUN apt-get update
RUN \
   apt-get install -y ruby ruby-dev make gcc nodejs && \
   gem install bundler && apt-get install -y npm && \
   ln -s /usr/bin/nodejs /usr/bin/node && npm install gulp -g && \
   apt-get install -y python-pip && pip install awscli
