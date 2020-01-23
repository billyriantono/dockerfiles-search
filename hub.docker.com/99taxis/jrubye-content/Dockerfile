FROM node:9-alpine

WORKDIR /app

RUN yarn global add pm2
COPY package.json /app/package.json
RUN yarn install
RUN mv /app/node_modules /node_modules

COPY . /app

CMD ["pm2-docker", "server.js"]
