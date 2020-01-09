FROM node:10
RUN mkdir -p /app

ADD . /app

WORKDIR /app

RUN yarn install

CMD ["yarn", "run", "production"]
