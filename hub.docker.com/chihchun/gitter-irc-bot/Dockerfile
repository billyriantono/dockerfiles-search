FROM node:latest
MAINTAINER Rex Tsai "http://about.me/chihchun"

WORKDIR /tmp
RUN npm install gitter-irc-bot@1.5.1 \
        && npm cache clear
CMD [ "node_modules/gitter-irc-bot/bin.js" ]
