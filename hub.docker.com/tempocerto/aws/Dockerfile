FROM alpine:3.8

RUN apk add --no-cache curl jq python py-pip \
    && pip install awscli \
    && rm -Rf ~/.cache/