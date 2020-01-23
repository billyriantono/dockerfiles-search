FROM node:8

RUN mkdir -p /opt/tslint
WORKDIR /opt/tslint

RUN npm i ava
ENTRYPOINT ["/opt/tslint/node_modules/.bin/ava"]

VOLUME /src
WORKDIR /src
