FROM golang:1.9.4-alpine3.7 AS build
RUN apk add --no-cache git
RUN CGO_ENABLED=0 go get github.com/prometheus/prometheus/documentation/examples/remote_storage/remote_storage_adapter

FROM scratch
COPY --from=build /go/bin/remote_storage_adapter  /bin/remote_storage_adapter
ENTRYPOINT ["/bin/remote_storage_adapter"]
