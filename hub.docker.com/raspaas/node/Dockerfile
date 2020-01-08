FROM node:0.12.7

ENV PORT 5000
EXPOSE 5000

RUN mkdir /app
WORKDIR /app

ONBUILD ADD ./package.json package.json
ONBUILD RUN npm install

ONBUILD ADD . /app
