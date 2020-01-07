# stage 0
FROM golang:latest as builder
WORKDIR /go/src/github.com/PierreZ/goStatic
COPY . .
RUN CGO_ENABLED=0 GOARCH=arm GOOS=linux go build -tags netgo -installsuffix netgo

# stage 1
FROM scratch
WORKDIR /
COPY --from=builder /go/src/github.com/PierreZ/goStatic/goStatic .
ENTRYPOINT ["/goStatic"]
