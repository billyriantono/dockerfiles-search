FROM node:12.6.0-alpine

ENV WEBAPP_DIR=/projects/face-recognition
ENV PATH /app/node_modules/.bin:$PATH

RUN mkdir -p $WEBAPP_DIR

WORKDIR $WEBAPP_DIR
COPY . $WEBAPP_DIR

RUN pwd
RUN ls
RUN npm i --silent
RUN npm install -g eslint-cli
RUN npm ls | grep react