FROM golang:1.10-alpine3.7 as builder

WORKDIR /app

RUN apk add --update git
RUN go get -d -v github.com/prometheus/prometheus/documentation/examples/remote_storage/remote_storage_adapter
RUN go build github.com/prometheus/prometheus/documentation/examples/remote_storage/remote_storage_adapter


FROM alpine:3.6

COPY --from=builder /app/remote_storage_adapter /

EXPOSE 9201

ENTRYPOINT ["/remote_storage_adapter"]