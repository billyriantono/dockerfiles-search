FROM golang:1.11.0-alpine3.8

RUN apk update && apk upgrade && apk add --no-cache bash git openssh
RUN wget https://s3.eu-west-2.amazonaws.com/nexus-cli/1.0.0-beta/linux/nexus-cli
RUN go get -u github.com/mlabouardy/nexus-cli