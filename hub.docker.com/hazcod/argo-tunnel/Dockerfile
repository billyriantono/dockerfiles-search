FROM golang:alpine AS builder

# Credits
LABEL maintainer="https://github.com/HazCod"

# Add prequisites and fetch go cpde
RUN apk add --no-cache ca-certificates git gcc build-base \
	&& go get -v github.com/cloudflare/cloudflared/cmd/cloudflared

# Switch to the working dir
WORKDIR /go/src/github.com/cloudflare/cloudflared/cmd/cloudflared

# Build a statical file
RUN CGO_ENABLED=0 GOOS=linux go build -o /go/bin/app -ldflags '-w -s -extldflags "-static"' /go/src/github.com/cloudflare/cloudflared/cmd/cloudflared

# Setup our scratch container
FROM scratch
COPY --from=builder /go/bin/app /app
COPY --from=builder /etc/ssl/certs/ /etc/ssl/certs/
ENTRYPOINT ["/app"]
