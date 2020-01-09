FROM hub.c.163.com/library/golang:latest
MAINTAINER goldwinner

RUN go get github.com/widuu/goini
RUN go get github.com/mikemintang/go-curl
RUN go get github.com/tidwall/gjson
RUN go get github.com/urfave/cli
RUN go get github.com/lib/pq
RUN go get github.com/go-redis/redis
RUN go get github.com/kataras/iris
RUN go get github.com/satori/go.uuid

WORKDIR $GOPATH

ADD run.sh /run.sh
RUN chmod 755 /run.sh
CMD ["/bin/bash","/run.sh"]
