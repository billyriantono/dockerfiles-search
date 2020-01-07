FROM golang:1.10 AS builder

ADD . /go/src/github.com/gitirabassi/nobind-initializer
WORKDIR /go/src/github.com/gitirabassi/nobind-initializer
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -o=nobind -a -ldflags '-extldflags "-static"' .

FROM gcr.io/distroless/base:latest
COPY --from=builder /go/src/github.com/gitirabassi/nobind-initializer/nobind /nobind
ENTRYPOINT [ "/nobind" ]
