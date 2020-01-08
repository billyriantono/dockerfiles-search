FROM golang:1.12-alpine AS build-env

ADD . /go/src/github.com/FingerLiu/soupbintcp
WORKDIR /go/src/github.com/FingerLiu/soupbintcp
RUN CGO_ENABLED=0 GOOS=linux go build -a -ldflags "-extldflags '-f'" -o sbtclient

FROM alpine
MAINTAINER liupeng.dalian@gmail.com

WORKDIR /

COPY --from=build-env /go/src/github.com/FingerLiu/soupbintcp/sbtclient ./sbtclient

ENTRYPOINT ["/sbtclient"]