FROM golang:1.6

COPY . /go/src/github.com/ofiliz/hello

WORKDIR /go/src/github.com/ofiliz/hello

RUN go install

CMD ["/go/bin/hello"]

