FROM golang:1.11.10-alpine3.9
LABEL maintainer="Siddhartha Basu <siddhartha-basu@northwestern.edu>"
RUN apk add --no-cache git build-base
RUN mkdir -p /modware-stock
WORKDIR /modware-stock
COPY go.mod ./
COPY go.sum ./
RUN go mod download
ADD cmd cmd
ADD internal internal
RUN go build -o app cmd/modware-stock/main.go

FROM alpine:3.9
RUN apk --no-cache add ca-certificates
COPY --from=0 /modware-stock/app /usr/local/bin/
ENTRYPOINT ["/usr/local/bin/app"]
