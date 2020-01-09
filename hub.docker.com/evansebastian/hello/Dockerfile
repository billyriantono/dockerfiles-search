FROM golang:1.10.0-stretch

ADD . /go/src/github.com/evansb/hello
RUN go install github.com/evansb/hello

ENTRYPOINT /go/bin/hello

EXPOSE 8080
