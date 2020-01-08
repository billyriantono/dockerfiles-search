FROM node
MAINTAINER Giambra Domenico <zorinik@gmail.com>

RUN apt-get update && apt-get -y upgrade

COPY app /app

WORKDIR /app
RUN npm install

EXPOSE 80

ENTRYPOINT ["node", "/app"]