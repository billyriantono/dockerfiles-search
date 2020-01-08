FROM alpine:3.9.2

COPY docker-tags /

RUN \
    apk add --no-cache curl jq && \
    adduser -D user

USER user

ENTRYPOINT ["/docker-tags"]
