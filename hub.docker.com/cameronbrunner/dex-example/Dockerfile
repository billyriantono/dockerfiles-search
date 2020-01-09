FROM golang:1.11.5-alpine

RUN apk add --no-cache --update alpine-sdk

COPY . /go/src/github.com/dexidp/dex
RUN cd /go/src/github.com/dexidp/dex && make

FROM alpine:3.8
# Dex connectors, such as GitHub and Google logins require root certificates.
# Proper installations should manage those certificates, but it's a bad user
# experience when this doesn't work out of the box.
#
# OpenSSL is required so wget can query HTTPS endpoints for health checking.
RUN apk add --update ca-certificates openssl

COPY --from=0 /go/src/github.com/dexidp/dex/bin/dex /usr/local/bin/dex
COPY --from=0 /go/src/github.com/dexidp/dex/bin/example-app /usr/local/bin/example-app

# Import frontend assets and set the correct CWD directory so the assets
# are in the default path.
COPY web /web
COPY examples /examples

COPY init.sh /init.sh

WORKDIR /

CMD ["/bin/sh", "/init.sh"]
