FROM rezzza/docker-node:latest

MAINTAINER Shaun Burdick <docker@shaunburdick.com>

RUN apk add -U tzdata

ENV NODE_ENV=production \
    SLACK_TOKEN=xoxb-398698793795-403238024229-tAArAq0mM6575nSAE7zKRKnr \
    SLACK_AUTO_RECONNECT=true \
    APP_ANNOUNCE_CHANNELS=general \
    APP_ANNOUNCE_TIMES=

ADD . /usr/src/myapp

WORKDIR /usr/src/myapp

RUN ["npm", "install"]

CMD ["npm", "start"]
