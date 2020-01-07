FROM resin/rpi-raspbian:latest
FROM node:carbon
WORKDIR /usr/src/app
COPY package*.json ./
RUN yarn
COPY . .
EXPOSE 1337
CMD ["yarn", "start"]
