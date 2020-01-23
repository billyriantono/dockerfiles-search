FROM node:10.15.2-alpine

COPY . /app
WORKDIR /app

RUN yarn install && yarn run build

ENV HOST 0.0.0.0
EXPOSE 3000

CMD ["yarn", "start"]
