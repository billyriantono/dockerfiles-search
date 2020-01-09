FROM node
MAINTAINER David Enke <post@davidenke.de>

ENV PARSE_DIR /parse

EXPOSE 1337

RUN mkdir -p $PARSE_DIR/cloud && touch $PARSE_DIR/cloud/main.js

WORKDIR $PARSE_DIR

ADD package.json $PARSE_DIR/
ADD index.js $PARSE_DIR/

VOLUME $PARSE_DIR/cloud
VOLUME $PARSE_DIR/logs

RUN npm install

CMD node . | node_modules/.bin/bunyan -Lo short
