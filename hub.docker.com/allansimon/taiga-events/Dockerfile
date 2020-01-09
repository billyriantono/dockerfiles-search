FROM node:alpine
MAINTAINER Allan Simon <allan.simon@supinfo.com>

RUN apk add --no-cache git bash sed

# EVENTS

WORKDIR /usr/src
RUN git clone -b master --single-branch --depth=1 https://github.com/taigaio/taiga-events.git taiga-events
WORKDIR /usr/src/taiga-events

RUN npm install --production
RUN npm install -g coffee-script

COPY config.json /usr/src/taiga-events/config.json

COPY docker-entrypoint.sh /docker-entrypoint.sh
RUN chmod +x /docker-entrypoint.sh

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["coffee", "index.coffee"]
