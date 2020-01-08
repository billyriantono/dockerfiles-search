FROM node:8

ADD yarn.lock /yarn.lock
ADD package.json /package.json

ENV NODE_PATH=/app/node_modules
ENV PATH=$PATH:/app/node_modules/.bin
RUN yarn

WORKDIR /app
ADD . /app

EXPOSE 3000

RUN yarn run build

CMD ["sh", "-c", "yarn run start"]
