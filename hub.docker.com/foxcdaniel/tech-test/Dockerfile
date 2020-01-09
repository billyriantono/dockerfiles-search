FROM alpine

RUN apk add --update nodejs

COPY ./src/ /app

WORKDIR /app

CMD node main.js

EXPOSE 8081