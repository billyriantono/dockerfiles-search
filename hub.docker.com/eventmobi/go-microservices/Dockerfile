FROM pallet/golang:12.04

MAINTAINER EventMobi Platform Team <platform@eventmobi.com>

ADD world.go /app/

WORKDIR /app

RUN go build -o world

CMD ["./world"]