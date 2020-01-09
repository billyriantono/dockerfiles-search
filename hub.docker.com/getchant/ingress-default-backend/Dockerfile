FROM golang:1-alpine as builder
COPY . $GOPATH/src/chant/api/
WORKDIR $GOPATH/src/chant/api/
RUN apk --no-cache add ca-certificates git
RUN go get -d -v
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o /main main.go

FROM scratch
WORKDIR /
COPY --from=builder /main .
COPY --from=builder /etc/ssl/certs /etc/ssl/certs
EXPOSE 80
CMD ["./main"]
