FROM golang:latest  AS builder
WORKDIR $GOPATH/src/github.com/hellodocker 
COPY .  .
RUN CGO_ENABLED=0 GOS=linux go build -a -installsuffix cgo -o \
hellodocker .
FROM alpine:latest
RUN apk --no-cache add ca-certificates
COPY --from=builder  /go/src/github.com/hellodocker .
CMD ["sh","-c","./hellodocker"]
