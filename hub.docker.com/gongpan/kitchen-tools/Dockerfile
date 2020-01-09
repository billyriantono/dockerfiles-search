FROM alpine

RUN apk upgrade --update

RUN apk add --update mysql-client

RUN apk add --update redis

RUN apk add --update curl 

RUN apk add bash

CMD [ "redis-cli" ]
