FROM alpine:3.7

RUN apk update \
    && apk upgrade --available --latest \
    && apk add --no-cache drill \
    && rm -rf /var/cache/apk/*

ENTRYPOINT ["/usr/bin/drill"]

CMD ["-h"]
