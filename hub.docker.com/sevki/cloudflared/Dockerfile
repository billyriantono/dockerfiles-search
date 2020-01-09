FROM golang:1.12 as builder
WORKDIR /go/src/github.com/cloudflare/cloudflared/
ADD . .
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o cloudflared ./cmd/cloudflared

FROM alpine:latest
RUN apk --no-cache add ca-certificates
WORKDIR /root/
COPY --from=0 /go/src/github.com/cloudflare/cloudflared/cloudflared .
CMD ["./cloudflared"]  