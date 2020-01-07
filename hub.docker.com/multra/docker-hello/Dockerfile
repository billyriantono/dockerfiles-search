FROM golang
MAINTAINER Multra <multra@gmail.com>
ADD . /go/src/github.com/golang/example/hello
RUN go install github.com/golang/example/hello
ENTRYPOINT /go/bin/hello
EXPOSE 8081
