FROM node:8.15.0-stretch
LABEL mantainer="Rafael Quintero <raf4.quintero@gmail.com>"

ARG HOME_PATH=/usr/src/app
RUN mkdir -p $HOME_PATH
WORKDIR $HOME_PATH

COPY . $HOME_PATH

RUN apt-get update -qq && apt-get install -y build-essential curl 

RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

RUN apt-get update && apt-get install -y yarn

RUN yarn install

EXPOSE 3000