FROM golang:1.13-alpine AS builder

# Install packages
RUN apk add --no-cache bash gcc musl-dev make git

# Install application
WORKDIR /go/src/github.com/mysteriumnetwork/quality-oracle
ADD . .

# Build application
RUN go run mage.go build

FROM alpine:3.9

# Install packages
RUN apk add --no-cache ca-certificates

# Install application
COPY --from=builder /go/src/github.com/mysteriumnetwork/quality-oracle/build/morqa /usr/bin/morqa

ENTRYPOINT ["/usr/bin/morqa"]
