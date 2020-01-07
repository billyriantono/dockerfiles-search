FROM alpine:3.8 AS base
RUN apk add --no-cache curl bash

FROM golang:1.11.4-alpine3.8 AS build-essential

FROM build-essential AS configure
RUN apk add --no-cache git
ENV GO111MODULE=on
ADD ./ ./src/cassandra-cluster
WORKDIR ./src/cassandra-cluster
RUN go mod download
RUN go mod tidy
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go install -i ./

FROM base
COPY --from=configure /go/bin/cassandra-cluster /cassandra-cluster
#CMD ["./cassandra-cluster"]
CMD ["top", "-b"]
