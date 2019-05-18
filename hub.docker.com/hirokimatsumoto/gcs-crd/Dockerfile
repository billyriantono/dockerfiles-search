# Build the manager binary
FROM golang:1.10.3-alpine as builder

# Copy in the go src
WORKDIR /go/src/github.com/h-r-k-matsumoto/gcs-crd
COPY pkg/    pkg/
COPY cmd/    cmd/
COPY vendor/ vendor/

# Build
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -a -o manager github.com/h-r-k-matsumoto/gcs-crd/cmd/manager

# Copy the controller-manager into a thin image
FROM scratch
WORKDIR /
COPY --from=builder /go/src/github.com/h-r-k-matsumoto/gcs-crd/manager .
ENTRYPOINT ["/manager"]
