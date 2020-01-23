FROM node:alpine

ENV NATS_URL nats://localhost:4222
ENV NATS_LIVE_START_SUBJECT games.csgo.parsers.hltv.live.*.start
ENV NATS_LIVE_EVENTS_SUBJECT games.csgo.parsers.hltv.live.*.events

WORKDIR /usr/src/app
COPY package.json yarn.lock ./
RUN yarn
COPY . ./

CMD ["node", "./src/index.js"]