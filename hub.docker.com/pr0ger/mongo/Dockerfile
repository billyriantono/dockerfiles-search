FROM alpine:latest

RUN apk --no-cache add mongodb

COPY mongod.conf /mongod.conf

EXPOSE 27017

VOLUME /data

ENTRYPOINT ["mongod", "--config", "/mongod.conf"]
