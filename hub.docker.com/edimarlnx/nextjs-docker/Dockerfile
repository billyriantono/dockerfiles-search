FROM node:8-alpine

COPY app /app

WORKDIR /app

RUN npm i -g yarn 

RUN yarn

CMD ["yarn", "start"]