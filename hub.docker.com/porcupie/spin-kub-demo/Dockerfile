FROM golang

ADD . /go/src/github.com/porcupie/spin-kub-demo

RUN go install github.com/porcupie/spin-kub-demo

ADD ./content /content

ENTRYPOINT /go/bin/spin-kub-demo
