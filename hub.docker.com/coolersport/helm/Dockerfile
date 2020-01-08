FROM alpine/helm:2.14.0

RUN apk upgrade && \
    addgroup -g 10000 jenkins && \
    adduser -u 10000 -G jenkins -s /bin/sh -D jenkins && \
    apk add --no-cache bash
