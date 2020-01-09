FROM node:slim

MAINTAINER Robert Brem <brem_robert@hotmail.com>

WORKDIR /var/www
ADD angular2-seed .
WORKDIR /var/www/angular2-seed
RUN npm install -g angular-cli

CMD ng serve
