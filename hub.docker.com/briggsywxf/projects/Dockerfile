# Base image
FROM node:10-alpine

# App directory
WORKDIR /usr/src/hex-server

# Install deps
COPY package.json ./
COPY yarn.lock ./
RUN yarn

COPY . .

EXPOSE 8080

CMD [ "node" , "server.js"]