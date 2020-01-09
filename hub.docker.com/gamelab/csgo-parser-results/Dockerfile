FROM node:alpine

ENV MONGO_DB gamelabs
ENV MONGO_COLLECTION csgo
ENV HLTV_URL_DIRECT http://localhost:4000/direct
ENV HLTV_URL_CACHE http://localhost:4000/cache
ENV OFFSET_START 0
ENV OFFSET_END 10

WORKDIR /app
COPY package.json yarn.lock ./
RUN yarn
COPY . ./

CMD ["node", "./src/index.js"]