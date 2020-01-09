FROM ghost:latest
MAINTAINER Thomas Vial
RUN npm i newrelic \
  && cp node_modules/newrelic/newrelic.js newrelic.js \
  && sed -i "1ivar newrelic = require('newrelic');" index.js \
  && touch /usr/src/ghost/newrelic_agent.log
