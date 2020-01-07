FROM golang as builder
WORKDIR /go/src/golangtest
ADD src /go/src
RUN go get ./... && CGO_ENABLED=0 GOOS=linux GOARCH=arm go build -a -installsuffix cgo -o app .

FROM scratch
COPY --from=builder /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/ca-certificates.crt
COPY --from=builder /go/src/golangtest/app /app
CMD ["/app"]
