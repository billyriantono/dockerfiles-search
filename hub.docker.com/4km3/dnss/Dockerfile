FROM alpine:3.6
MAINTAINER pancho horrillo <pancho@pancho.name>

RUN set -e;                                                                   \
    apk add --no-cache ca-certificates git go gcc musl-dev;                   \
    GOPATH=/tmp/go GOBIN=/ go get -v -ldflags '-s' blitiri.com.ar/go/dnss;    \
    apk del git go gcc musl-dev;                                              \
    rm -rf /tmp/go

EXPOSE 53

ENTRYPOINT ["/dnss"]
