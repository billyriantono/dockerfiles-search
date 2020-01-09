FROM golang as build

LABEL maintainer="admin@diamondyuan.com"

ENV CGO_ENABLED=0

WORKDIR  /yuanlimanman

ADD main.go /yuanlimanman/

RUN go get github.com/jinzhu/now && \
	go build

FROM alpine

COPY --from=build /yuanlimanman/yuanlimanman /usr/bin/

RUN apk update && \
    apk add ca-certificates

WORKDIR /

ENTRYPOINT ["yuanlimanman"]
