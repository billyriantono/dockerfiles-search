FROM alpine

RUN apk add \
    --no-cache \
    --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing \
    git git-secret gawk

ENTRYPOINT ["/usr/bin/git", "secret"]
