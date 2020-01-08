FROM node:latest

RUN mkdir /app
WORKDIR /app
COPY . /app

RUN npm install

EXPOSE 8080
CMD bin/hubot -a slack
