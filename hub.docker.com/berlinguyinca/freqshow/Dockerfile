FROM node:8.11.3-alpine
MAINTAINER berlinguyinca@gmail.com
EXPOSE 8080
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app
ADD . /usr/src/app
RUN npm install -g @angular/cli
RUN npm rebuild --force
RUN npm install
RUN ng build
CMD ["node", "server.js"]
