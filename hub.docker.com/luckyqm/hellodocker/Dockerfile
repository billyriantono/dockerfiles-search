FROM golang:latest as builder

WORKDIR /go/src/luckyzune.com/mq/hellodocker
ADD . /go/src/luckyzune.com/mq/hellodocker

RUN go-wrapper download
RUN go build -v

FROM buildpack-deps:jessie

WORKDIR /usr/local/bin
COPY --from=builder /go/src/luckyzune.com/mq/hellodocker/hellodocker .
EXPOSE 8000
CMD ["./hellodocker"]
