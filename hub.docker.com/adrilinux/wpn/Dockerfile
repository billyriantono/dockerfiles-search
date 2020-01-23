FROM golang:1.10-alpine as builder
RUN apk add -U --no-cache git build-base sqlite-dev ca-certificates
RUN go get github.com/theSuess/wpn
WORKDIR /go/src/github.com/theSuess/wpn
RUN CGO_ENABLED=0 GOOS=linux go build -v -o wpn .

FROM scratch
COPY --from=builder /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/
COPY --from=builder /go/bin/wpn /usr/bin/
#EXPOSE 8000 9000 80 443
ENTRYPOINT ["wpn"]

