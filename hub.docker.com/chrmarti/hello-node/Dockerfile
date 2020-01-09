FROM node:7.9.0-alpine

MAINTAINER Christof Marti <chrmarti@microsoft.com>

WORKDIR /app

RUN npm install -g nodemon

COPY package.json /app/package.json
RUN npm install

COPY . /app

EXPOSE 3000 9229

CMD ["npm", "start"]