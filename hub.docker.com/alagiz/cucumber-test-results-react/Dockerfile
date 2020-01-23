FROM node:9.6.1

RUN mkdir /usr/src/app
WORKDIR /usr/src/app
COPY /komkommer-react/public /usr/src/app/public
COPY /komkommer-react/src /usr/src/app/src

ENV PATH /usr/src/app/node_modules/.bin:$PATH

COPY /komkommer-react/package.json /usr/src/app/package.json

RUN npm install --silent