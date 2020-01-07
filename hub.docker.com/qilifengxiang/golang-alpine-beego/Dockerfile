FROM golang:alpine
RUN apk add git && \
    go get github.com/astaxie/beego && \
    mkdir -p /go/src/golang.org/x/time && \
    git clone  https://github.com/golang/time.git /go/src/golang.org/x/time && \
    go get github.com/astaxie/beego/config/yaml && \
    go get github.com/aliyun/aliyun-oss-go-sdk/oss
