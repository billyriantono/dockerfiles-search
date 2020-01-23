FROM node:11-alpine

EXPOSE 8080

WORKDIR /usr/src/app
COPY . .

RUN npm install

ENV HELLO_VAR allir

CMD [ "npm", "start" ]

