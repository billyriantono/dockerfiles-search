FROM node:alpine

COPY . /src

RUN cd /src; npm install

EXPOSE 8080

CMD cd /src && node ./app.js
