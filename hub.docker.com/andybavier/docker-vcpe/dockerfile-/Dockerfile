FROM node:12
MAINTAINER Giambra Domenico <zorinik@gmail.com>

RUN apt-get update && apt-get -y upgrade

EXPOSE 80

COPY app /app

WORKDIR /app
RUN npm ci

ENTRYPOINT ["node", "/app"]
