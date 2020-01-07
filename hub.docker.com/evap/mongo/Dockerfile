FROM alpine:edge
RUN mkdir -p /data/db
RUN echo 'http://dl-3.alpinelinux.org/alpine/edge/testing' >> /etc/apk/repositories
RUN apk upgrade --update
RUN apk add mongodb

EXPOSE 27017 28017

ENTRYPOINT ["mongod"]
