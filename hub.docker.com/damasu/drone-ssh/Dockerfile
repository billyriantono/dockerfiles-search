FROM golang:latest

MAINTAINER Jesse Quinn <me@jessequinn.info>

RUN mkdir /app
ADD . /app/
WORKDIR /app
RUN go install

ENV GOOS=linux
ENV GOARCH=amd64
ENV CGO_ENABLED=0
ENV GO111MODULE=on

RUN go build -v -a -tags netgo -o release/linux/amd64/drone-ssh .

CMD ["/app/release/linux/amd64/drone-ssh"]
