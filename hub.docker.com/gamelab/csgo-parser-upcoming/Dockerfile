FROM node:alpine

ENV NATS_URL nats://localhost:4222
ENV NATS_UPCOMING_SUBJECT games.csgo.parsers.upcoming
ENV HLTV_URL_DIRECT http://localhost:4000/direct

WORKDIR /usr/src/app
COPY package.json yarn.lock ./
RUN yarn
COPY . ./

CMD ["node", "./src/index.js"]