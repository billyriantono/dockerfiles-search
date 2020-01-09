FROM node:7-slim

MAINTAINER Jiri Kratochvil <jiri@kratochvil.eu>

WORKDIR /app
ADD package.json package.json
RUN npm install

VOLUME ["/app/data"]

EXPOSE 5000

ADD . .

CMD npm start

