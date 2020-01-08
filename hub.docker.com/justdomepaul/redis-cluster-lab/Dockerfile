FROM alpine:3.8 AS base
RUN apk add --no-cache curl bash

FROM golang:1.11.4-alpine3.8 AS build-essential

FROM build-essential AS configure
RUN apk add --no-cache git
ENV GO111MODULE=on
ADD ./ ./src/redis-cluster
WORKDIR ./src/redis-cluster
RUN go mod download
RUN go mod tidy
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go install -i ./

FROM base
COPY --from=configure /go/bin/redis-cluster /redis-cluster
#CMD ["./redis-cluster"]
CMD ["top", "-b"]
