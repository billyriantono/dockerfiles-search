FROM golang:1.12.9@sha256:584daefca21d7b8f0702e70bfe6a31c3a6def12ed4145a8d6fe78c205f124f1e as builder
WORKDIR /builder/
COPY . .

RUN CGO_ENABLED=0 \
    GOOS=linux \
    go build \
    -a \
    -installsuffix cgo \
    -o marketplace-oauth \
    cmd/marketplace_oauth/main.go

FROM alpine:3.10.1@sha256:6a92cd1fcdc8d8cdec60f33dda4db2cb1fcdcacf3410a8e05b3741f44a9b5998
RUN apk --no-cache add ca-certificates
WORKDIR /bin/
# Copy the Pre-built binary file from the previous stage
COPY --from=builder /builder/marketplace-oauth .
EXPOSE 8080
CMD ["./marketplace-oauth"]
