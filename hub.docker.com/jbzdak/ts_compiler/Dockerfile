FROM node:7.6-alpine

RUN npm install -g typescript@${TYPESCRIPT_VERSION:-2.2.2}

CMD tsc

VOLUME ['/app']

WORKDIR /app
