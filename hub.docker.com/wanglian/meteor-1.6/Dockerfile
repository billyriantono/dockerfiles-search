FROM node:8.9.4

RUN curl https://install.meteor.com/?release=1.6 | sh \
  && apt-get update \
  && apt-get install -y build-essential g++ \
  && npm install -g npm \
  && npm install -g mup
