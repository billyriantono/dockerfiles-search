FROM golang:latest as builder
WORKDIR /go/src/github.com/tzapil/english
COPY . .
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -ldflags '-s' -o ./bin/english

FROM scratch
COPY --from=builder /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/
COPY --from=builder /go/src/github.com/tzapil/english/bin/english .

EXPOSE 8080
ENTRYPOINT ["./english"]
