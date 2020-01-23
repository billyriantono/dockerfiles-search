FROM golang:1.10.3
WORKDIR /go/src/app

COPY vendor/src /go/src
COPY src/server/* ./

RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o app

FROM scratch

EXPOSE 53/tcp 53/udp

COPY --from=0 /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/ca-certificates.crt
COPY etc/config.yaml /etc/config.yaml
COPY --from=0 /go/src/app/app .

CMD ["./app"]
