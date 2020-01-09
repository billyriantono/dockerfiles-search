FROM node:11.3.0-alpine

RUN mkdir -p /usr/src/ui
WORKDIR /usr/src/ui

# add `/usr/src/ui/node_modules/.bin` to $PATH
ENV PATH /usr/src/ui/node_modules/.bin:$PATH

# install and cache ui dependencies

ENV APP_HOME /usr/src/ui
RUN npm install -g yarn

COPY package.json $APP_HOME/package.json
RUN npm install
COPY . $APP_HOME

ENTRYPOINT ["yarn", "start"]
