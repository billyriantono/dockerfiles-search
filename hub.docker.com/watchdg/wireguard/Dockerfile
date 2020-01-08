FROM alpine:3.10
RUN apk update && apk add --no-cache bash openresolv wireguard-tools
COPY docker-entrypoint.sh .
ENTRYPOINT ["/docker-entrypoint.sh"]
