FROM golang:latest

ENV GOPATH /go

RUN apt-get update && \
    apt-get upgrade -y

# install revel and revel-cli
RUN go get github.com/revel/revel && \
    go get github.com/revel/cmd/revel

RUN mkdir /go/src/portfolio
WORKDIR /go/src/portfolio
COPY ./ /go/src/portfolio

RUN go get -v ./...

CMD ["revel", "run", "portfolio"]

EXPOSE 9000
