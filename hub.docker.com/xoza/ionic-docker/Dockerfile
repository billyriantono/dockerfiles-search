FROM node:10

RUN apt-get -y update \
    && apt-get -y install chromium

RUN npm i npm -g \
    && npm i ionic cordova -g

ENV CHROME_BIN=/usr/bin/chromium

WORKDIR /app
