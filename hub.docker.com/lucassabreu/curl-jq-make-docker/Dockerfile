FROM alpine:latest

RUN apk add -u curl jq make && rm -rf /var/cache/apk/*

ENTRYPOINT ["make"]
