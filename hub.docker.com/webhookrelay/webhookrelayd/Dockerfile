# Creates relayd daemon image

FROM golang:1.11.2-alpine
COPY . /go/src/github.com/rusenask/client
WORKDIR /go/src/github.com/rusenask/client
RUN apk add --no-cache git \
    make
RUN make relayd

FROM alpine:latest
RUN apk --no-cache add ca-certificates
COPY --from=0 /go/src/github.com/rusenask/client/cmd/relayd/relayd /relayd
ENTRYPOINT ["/relayd"]