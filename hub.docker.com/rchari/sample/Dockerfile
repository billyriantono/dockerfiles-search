FROM golang:1.10-alpine3.8 as gobox
ADD main.go .

RUN go build main.go



FROM alpine:3.8

COPY --from=gobox /go/main /root/dev/
RUN chmod +x /root/dev/main

EXPOSE 80

CMD ["/root/dev/main"]
