FROM node:7.10.1-alpine
ENV NPM_CONFIG_LOGLEVEL=warn
RUN npm i -g pm2
EXPOSE 3000
ENV DIR /usr/src/app
RUN mkdir -p $DIR
WORKDIR $DIR
COPY . $DIR
RUN npm install
RUN $DIR/node_modules/.bin/clap build
CMD pm2-runtime ./lib/server/index.js