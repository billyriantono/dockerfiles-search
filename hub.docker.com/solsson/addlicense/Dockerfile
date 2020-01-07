FROM golang:1.13.3-alpine3.10@sha256:40278d43a27b6e0563fcc4dd52c991a25741b1a775402aea342ab9a80158e69e

RUN apk add --no-cache git

RUN go get -u github.com/google/addlicense

RUN which addlicense

FROM alpine:3.10@sha256:c19173c5ada610a5989151111163d28a67368362762534d8a8121ce95cf2bd5a

COPY --from=0 /go/bin/addlicense /usr/local/bin/addlicense

ENTRYPOINT [ "addlicense" ]

WORKDIR /workspace/source
