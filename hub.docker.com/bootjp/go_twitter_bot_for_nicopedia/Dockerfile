FROM golang:1.11 as builder
WORKDIR /go/src/tiedot/
COPY ./    .
WORKDIR /go/
RUN go get -v -d tiedot
RUN CGO_ENABLED=0 GOOS=linux go install -a -installsuffix cgo -v tiedot

FROM alpine:latest
RUN apk --no-cache add ca-certificates
WORKDIR /root/
COPY --from=builder /go/bin/tiedot /bin/
RUN chmod +x /bin/tiedot
EXPOSE 3661
VOLUME ["/data"]
CMD ["/bin/tiedot","-dir","/data","-port","3661","-mode","httpd"]
