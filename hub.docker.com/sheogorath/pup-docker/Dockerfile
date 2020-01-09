FROM alpine:3.7

ARG VERSION=v0.4.0

RUN apk add --no-cache --virtual .build-utils wget ca-certificates && \
    wget "https://github.com/ericchiang/pup/releases/download/$VERSION/pup_${VERSION}_linux_amd64.zip" && \
    unzip "pup_${VERSION}_linux_amd64.zip" && \
    rm "pup_${VERSION}_linux_amd64.zip" && \
    apk del .build-utils && \
    chmod +x pup

ENTRYPOINT ["/pup"]
