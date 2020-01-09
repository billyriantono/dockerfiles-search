FROM golang:1.7.3 as builder



RUN go get -d -v golang.org/x/net/html  
RUN go get -u -v github.com/alexellis/href-counter
WORKDIR /go/src/github.com/alexellis/href-counter

FROM alpine:latest  
RUN apk --no-cache add ca-certificates

WORKDIR /root/

COPY --from=builder /go/bin/href-counter .

CMD ["./app"]  
