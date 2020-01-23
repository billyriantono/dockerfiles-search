FROM golang:1.11.4 as builder
WORKDIR /go/src/github.com/omarpando/test/
COPY main.go .
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o app .

FROM alpine:latest  
RUN apk --no-cache add ca-certificates
WORKDIR /root/
COPY --from=builder /go/src/github.com/omarpando/test/app .
CMD ["./app"]  