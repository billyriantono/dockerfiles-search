FROM golang:1.12.0-alpine3.9
WORKDIR /go/src/github.com/pagarme/watcher
RUN apk --no-cache add curl git
RUN curl -fsSL -o /usr/local/bin/dep https://github.com/golang/dep/releases/download/v0.5.0/dep-linux-amd64 && chmod +x /usr/local/bin/dep
COPY Gopkg.toml Gopkg.lock ./
RUN dep ensure -vendor-only
COPY . .
RUN CGO_ENABLED=0 GOOS=linux go build -ldflags "-s -w" -a -installsuffix cgo -o watcher .

FROM alpine:3.9
RUN apk --no-cache add ca-certificates
WORKDIR /root/
COPY --from=0 /go/src/github.com/pagarme/watcher .
CMD ["./watcher"]
