FROM golang:alpine

RUN apk add --no-cache git ca-certificates make
RUN git clone https://github.com/OJ/gobuster.git

WORKDIR /go/gobuster

RUN go get github.com/OJ/gobuster
RUN go build
RUN make linux

ADD ./data/wordlists /data/wordlists

ENTRYPOINT ["/go/gobuster/gobuster"]
