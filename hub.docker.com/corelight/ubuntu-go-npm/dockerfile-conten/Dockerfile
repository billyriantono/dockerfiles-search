FROM golang:alpine as builder

RUN set -x\
 && apk add --no-cache\
    gcc\
    git\
    linux-headers\
    musl-dev\
 && go get github.com/keybase/client/go/keybase\
 && go install -tags production github.com/keybase/client/go/keybase\
 && cd /go/src/github.com/keybase/client\
 && echo "$(/go/bin/keybase -version | sed 's/.* //')-$(git rev-parse --short HEAD)" >> /tmp/keybase_client_version

FROM alpine:edge

COPY --from=builder /tmp/keybase_client_version /tmp/keybase_client_version
COPY --from=builder /go/bin/keybase /usr/bin/keybase

RUN echo "KEYBASE_VERSION=$(cat /tmp/keybase_client_version)" >> /etc/profile\
 && rm /tmp/keybase_client_version

ENTRYPOINT ["keybase"]
CMD ["--version"]
