FROM alpine:latest

MAINTAINER Andrew Cutler <andrew@panubo.com>

RUN apk add --update bash gzip openssh-client rsync && \
    rm -rf /var/cache/apk/*

COPY commands /commands

ENTRYPOINT ["/commands/entry.sh"]

CMD ["default"]
