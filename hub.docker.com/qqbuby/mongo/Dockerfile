FROM alpine:3.6 as extract
LABEL maintainer="ROY <qqbuby@gmail.com>"

RUN apk add --no-cache xz

WORKDIR /db

COPY ./mongodb-linux-x86_64-2.6.12.tar.xz .

RUN tar xvf mongodb-linux-x86_64-2.6.12.tar.xz

FROM buildpack-deps:stretch-scm

# add our user and group first to make sure their IDs get assigned consistently, regardless of whatever dependencies get added
RUN groupadd -r mongodb && useradd -r -g mongodb mongodb

COPY --from=extract /db/mongodb-linux-x86_64-2.6.12/bin /usr/local/bin

RUN mkdir -p /data/db /data/configdb \
    && chown -R mongodb:mongodb /data/db /data/configdb

VOLUME /data/db /data/configdb

EXPOSE 27017

CMD ["mongod"]
