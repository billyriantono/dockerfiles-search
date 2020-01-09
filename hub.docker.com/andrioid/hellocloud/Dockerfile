FROM golang
ADD . /go/src/github.com/andrioid/hellocloud
RUN go install github.com/andrioid/hellocloud

ENTRYPOINT /go/bin/hellocloud

EXPOSE 9999