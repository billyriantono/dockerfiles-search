FROM golang:1.8.3-alpine as builder

ARG APP_VERSION=0.0.1

# copy code
ADD . /go/src/bitbucket.org/thilinaperera/mongo-bootstrap

# solution root
WORKDIR /go/src/bitbucket.org/thilinaperera/mongo-bootstrap

# pull deps
RUN apk add --no-cache --virtual git
RUN go get -u github.com/golang/dep/cmd/dep
RUN dep ensure

# output
RUN mkdir /go/dist
RUN go build -ldflags "-X main.version=$APP_VERSION" \
    -o /go/dist/bootstrap bitbucket.org/thilinaperera/mongo-bootstrap

FROM alpine:latest

COPY --from=builder /go/dist/bootstrap /mongo-swarm/bootstrap

RUN chmod 777 /mongo-swarm/bootstrap

EXPOSE 9090
WORKDIR /mongo-swarm
ENTRYPOINT ["/mongo-swarm/bootstrap"]
