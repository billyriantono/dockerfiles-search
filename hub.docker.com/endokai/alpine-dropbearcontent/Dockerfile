FROM golang:alpine AS build

WORKDIR /go/src

ADD ./ ./monitor

RUN sed -i "s/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g" /etc/apk/repositories \
    && apk update && apk add --no-cache git upx \
    && git clone https://github.com/golang/sys.git $GOPATH/src/golang.org/x/sys \
    && go get github.com/sirupsen/logrus \
    && go get github.com/streadway/amqp \
    && CGO_ENABLED=0 go build -ldflags '-w -s' -o server monitor \
    && upx server

FROM alpine

ENV TZ Asia/Shanghai

WORKDIR /usr/local/bin

COPY --from=build /go/src/server .

RUN apk update \
    && apk add tzdata --no-cache \
    && cp /usr/share/zoneinfo/$TZ /etc/localtime \
    && echo $TZ > /etc/timezone \
    && rm -rf /var/cache/apk

CMD ["./server"]