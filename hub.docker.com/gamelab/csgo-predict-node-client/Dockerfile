FROM node:alpine

ENV NODE_PATH src/
ENV NATS_URL nats://127.0.0.1:4222
ENV NATS_PREDICT_NODE_SUBJECT games.csgo.predict.node

WORKDIR /usr/src/app
COPY . ./
RUN yarn
RUN yarn build


EXPOSE 8080
CMD ["yarn", "run", "server"]
