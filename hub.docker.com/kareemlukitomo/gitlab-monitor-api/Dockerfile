FROM node:11-alpine

WORKDIR /app

COPY . ./

RUN yarn --production=false

CMD [ "yarn", "start" ]