FROM golang:1.9.4-alpine
MAINTAINER fukun fukun@360.cn

#使用阿里云镜像源，加快国内访问速度
RUN echo 'http://mirrors.aliyun.com/alpine/latest-stable/main/' > /etc/apk/repositories; \
        echo 'http://mirrors.aliyun.com/alpine/latest-stable/community/' >> /etc/apk/repositories; \
        apk update;
RUN apk add --update git
RUN go get -u github.com/golang/dep/cmd/dep

