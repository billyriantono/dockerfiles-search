FROM node:6.9.2-wheezy
MAINTAINER Guillaume Giordana <guillaume.giordana@the-oz.com>

RUN npm install -g nodemon

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app
VOLUME /usr/src/app

ENV NODE_ENV production

EXPOSE 8000

CMD ["nodemon", "-L", "/usr/src/app"]



