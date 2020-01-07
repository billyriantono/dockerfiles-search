FROM alpine:3.5

LABEL maintainer="devops@zappistore.com"

ARG GOPATH="/go"

RUN apk update && \
    apk upgrade && \
    apk --virtual build-deps add \
      go>1.6 curl git gcc musl-dev make && \
    apk add \
      python py-pip bash && \
    pip install --upgrade pip envtpl && \
    go get -u github.com/influxdata/influxdb-relay && \
    cp $GOPATH/bin/influxdb-relay /usr/local/bin && \
    apk del build-deps && \
    rm -rf /var/cache/apk/* $GOPATH/*

EXPOSE 9096

COPY relay.toml /etc/relay.toml.tpl
COPY run.sh /bin/

ENTRYPOINT ["/bin/sh", "-c"]
CMD ["/bin/run.sh"]
