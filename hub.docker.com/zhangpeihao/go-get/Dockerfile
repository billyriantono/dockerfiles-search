FROM golang:1.4
MAINTAINER Zhang Peihao "zhangpeihao@gmail.com"

RUN go get -u -tags "sqlite redis memcache" github.com/gogits/gogs

VOLUME ["/shared"]

CMD /bin/bash
