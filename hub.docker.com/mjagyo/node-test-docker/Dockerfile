FROM node:8.11.1-alpine
MAINTAINER Mark Joseph Jagyo
COPY . /src
RUN cd /src; npm install
EXPOSE 9112
CMD cd /src && node ./app.js