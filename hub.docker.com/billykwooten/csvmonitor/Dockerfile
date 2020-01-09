# Create Builder & Build
FROM golang:1.12.1-alpine3.9 as builder

RUN apk update && apk add --no-cache git && apk add ca-certificates
RUN adduser -D -g '' appuser

COPY . $GOPATH/src/github.com/billykwooten/csvmonitor
WORKDIR $GOPATH/src/github.com/billykwooten/csvmonitor

# Get Dependencies
ENV GO111MODULE=on
RUN go mod vendor

# Build Binary in builder
RUN CGO_ENABLED=0 GOOS="linux" GOARCH="amd64" go build -a -installsuffix cgo -ldflags="-w -s" -o /app

# Create Container
FROM scratch

MAINTAINER Billy Wooten <billykwooten@gmail.com>

COPY --from=builder /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/
COPY --from=builder /etc/passwd /etc/passwd
COPY --from=builder /app /app

USER appuser
ENTRYPOINT ["/app"]