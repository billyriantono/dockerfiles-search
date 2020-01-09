FROM golang:1.13.4

COPY go.mod /go.mod
COPY blue/main.go /main.go

WORKDIR /

RUN set -x \
 && go build -o color .

EXPOSE 80

CMD ["/color"]
