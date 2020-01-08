FROM node:11-alpine

MAINTAINER ArthurWang "yahui9119@live.com"

RUN npm install -g yarn  pm2

VOLUME ["/app"]
ADD start /start
RUN chmod 755 /start
CMD ["/start"]
