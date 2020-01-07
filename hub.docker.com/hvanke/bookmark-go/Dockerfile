FROM golang:1.11.4

WORKDIR /go/src/app

ADD . /go/src/app

RUN export GO111MODULE=on && go mod tidy && go mod download && go mod vendor && go build -o main .

EXPOSE 4001

# must be ENTRYPOINT
ENTRYPOINT ["./main"]
