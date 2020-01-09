FROM node:10.15.3
MAINTAINER kuliahonline <kulon@kuliahonline.com>

RUN apt-get update -y && apt-get install rsync -y
RUN npm install pm2 -g

VOLUME ["/app"]

WORKDIR /app