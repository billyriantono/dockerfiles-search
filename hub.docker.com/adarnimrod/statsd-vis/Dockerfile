FROM golang:alpine as go-statsd-vis
RUN apk --update add git && \
    rm -rf /var/cache/apk/* && \
    /usr/local/go/bin/go get github.com/rapidloop/statsd-vis

FROM alpine
COPY --from=go-statsd-vis /go/bin/statsd-vis /usr/local/bin
USER nobody
EXPOSE 8080/tcp 8125/tcp 8125/udp
CMD [ "/usr/local/bin/statsd-vis", "-statsdudp", "0.0.0.0:8125", "-statsdtcp", "0.0.0.0:8125" ]
HEALTHCHECK CMD wget --quiet --spider http://localhost:8080/ || exit 1
