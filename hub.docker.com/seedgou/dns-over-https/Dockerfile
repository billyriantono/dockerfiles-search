FROM golang:alpine as builder

RUN apk add --update \
    git make \
  && rm -rf /var/cache/apk/*

RUN git clone https://github.com/m13253/dns-over-https.git /dns-over-https

WORKDIR /dns-over-https

RUN make

FROM alpine

COPY --from=builder /dns-over-https/doh-server/doh-server /doh-server
COPY --from=builder /dns-over-https/doh-client/doh-client /doh-client

COPY ./doh-server.conf /doh-server.conf
COPY ./doh-client.conf /doh-client.conf
