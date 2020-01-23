FROM golang:1.11.1-alpine AS builder

# Install packages
RUN apk add --no-cache bash gcc musl-dev make git

# Compile application
WORKDIR /go/src/github.com/mysteriumnetwork/morqa
ADD . .
RUN make build

FROM alpine:3.8

# Install packages
RUN apk add --no-cache ca-certificates

# Install application
COPY --from=builder /go/src/github.com/mysteriumnetwork/morqa/build/morqa /usr/bin/morqa

ENTRYPOINT ["/usr/bin/morqa"]
