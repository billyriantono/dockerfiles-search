FROM golang:1.13.1-alpine3.10 AS builder

WORKDIR /go/src/registrator/

COPY . .

RUN \
	apk add --no-cache curl git \
	&& curl https://raw.githubusercontent.com/golang/dep/master/install.sh | sh \
	&& dep ensure -vendor-only \
	&& CGO_ENABLED=0 GOOS=linux go build \
		-a -installsuffix cgo \
		-ldflags "-X main.Version=$(cat VERSION)" \
		-o bin/registrator \
		.

# ---

FROM alpine:3.7

RUN apk add --no-cache ca-certificates

COPY --from=builder /go/src/registrator/bin/registrator /bin/registrator

ENTRYPOINT ["/bin/registrator"]
