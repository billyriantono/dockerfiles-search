FROM alpine:latest
RUN apk add --update curl openssl dumb-init && rm -rf /var/cache/apk/*
ENTRYPOINT [ "/usr/bin/dumb-init", "curl" ]
CMD ["--help"]
