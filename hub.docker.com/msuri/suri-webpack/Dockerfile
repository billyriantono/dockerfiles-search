FROM node:11.15.0
MAINTAINER Marc Sureda <surikata@gmail.com>

RUN npm install -g webpack@4.31.0 webpack-dev-server@3.3.1 yarn@1.16.0 @angular/cli@8.1.0 react@16.8.6
RUN chmod 777 /usr/local/bin/yarn

VOLUME /app

EXPOSE 3000

WORKDIR /app