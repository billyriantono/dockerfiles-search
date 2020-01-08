# Build Gunc in a stock Go builder container
FROM golang:1.10-alpine as builder

RUN apk add --no-cache make gcc musl-dev linux-headers

ADD . /uncommons
RUN cd /uncommons && make gunc

# Pull Gunc into a second stage deploy alpine container
FROM alpine:latest

RUN apk add --no-cache ca-certificates
COPY --from=builder /uncommons/build/bin/gunc /usr/local/bin/

EXPOSE 8646 8647 31313 31313/udp
ENTRYPOINT ["gunc"]
