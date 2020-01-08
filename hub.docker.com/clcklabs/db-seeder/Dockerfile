FROM node:10-alpine

WORKDIR /app

COPY package.json /app
COPY bin /app/bin
COPY modules /app/modules
COPY app.js /app
COPY index.js /app

RUN npm install
RUN npm audit fix

ENTRYPOINT [ "/app/bin/db-seeder" ]