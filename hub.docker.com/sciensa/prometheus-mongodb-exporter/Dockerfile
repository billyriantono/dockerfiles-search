FROM golang:alpine

RUN apk add --update ca-certificates
RUN apk --no-cache add curl git make perl
RUN curl -s https://glide.sh/get | sh
COPY . /go/src/github.com/dcu/mongodb_exporter
RUN cd /go/src/github.com/dcu/mongodb_exporter && make build


RUN mv /go/src/github.com/dcu/mongodb_exporter/mongodb_exporter /usr/local/bin/mongodb_exporter

EXPOSE 9001

ENTRYPOINT [ "mongodb_exporter" ]
