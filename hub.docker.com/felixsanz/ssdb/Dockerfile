FROM alpine:latest

MAINTAINER Félix Sanz <me@felixsanz.com>

RUN apk update

RUN apk add gcc

RUN apk add --virtual .build-deps autoconf make g++ git

RUN mkdir -p /usr/src/ssdb

RUN git clone --depth 1 https://github.com/ideawu/ssdb.git /usr/src/ssdb && \
  make -C /usr/src/ssdb && \
  make -C /usr/src/ssdb install && \
  rm -rf /usr/src/ssdb

RUN apk del .build-deps

COPY ssdb.conf /usr/local/ssdb/ssdb.conf

EXPOSE 8888

RUN mkdir /data

VOLUME /data

WORKDIR /data

CMD ["/usr/local/ssdb/ssdb-server", "/usr/local/ssdb/ssdb.conf"]
