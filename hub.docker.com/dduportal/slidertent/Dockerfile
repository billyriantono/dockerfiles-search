FROM golang:1.3

RUN apt-get update && apt-get install -y iptables
RUN go get code.google.com/p/go.tools/cmd/cover
RUN go get github.com/modocache/gover
RUN go get github.com/mattn/goveralls
