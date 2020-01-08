FROM golang:latest

COPY . /go/src/github.com/mach16/go-annie

RUN go install github.com/mach16/go-annie/cmd/annie

ENTRYPOINT /go/bin/annie
