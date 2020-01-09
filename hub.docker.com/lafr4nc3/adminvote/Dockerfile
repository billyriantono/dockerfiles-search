FROM node:9-alpine

RUN mkdir -p /app
COPY . /app
WORKDIR /app


RUN yarn install && yarn cache clean

CMD ["yarn", "start"]
