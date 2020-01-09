FROM node:8-alpine
MAINTAINER Michael Tom-Wing <mtomwing@gmail.com>

EXPOSE 5050

RUN npm install -g sonos-web-cli
RUN sonos-web install

WORKDIR /root/.sonos-web
CMD ["node", "src/server.js"]
