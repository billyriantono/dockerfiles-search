FROM node:alpine

WORKDIR /app

COPY ./bitso-front/ ./


WORKDIR /app/bitso-front

run npm install

CMD [ "npm", "run", "test" ]
