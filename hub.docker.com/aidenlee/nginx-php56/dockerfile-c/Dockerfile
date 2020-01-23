# Build step
FROM golang:1.13 AS builder
ADD src /mnt
WORKDIR /mnt
RUN go mod download
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -a -o /usr/bin/shtbot .
RUN chmod +X /usr/bin/shtbot 

FROM scratch
COPY --from=builder /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/ca-certificates.crt
COPY --from=builder /usr/bin/shtbot /shtbot
ENTRYPOINT ["/shtbot"]
EXPOSE 8080