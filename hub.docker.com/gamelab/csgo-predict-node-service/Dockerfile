FROM node:latest

ENV NATS_URL nats://127.0.0.1:4222
ENV NATS_PREDICT_NODE_SUBJECT games.csgo.predict.node
ENV MONGO_URL mongodb://gamelabs:gamelabs@gamelabs.kabelsea.ru:27017?authSource=gamelabs
ENV MONGO_DB gamelabs
ENV MONGO_COLLECTION csgo
ENV TRAIN_TEAMS 256
ENV TRAIN_SAMPLE 4000

WORKDIR /usr/src/app
COPY . ./
RUN yarn
RUN yarn run train

CMD ["yarn", "start"]
