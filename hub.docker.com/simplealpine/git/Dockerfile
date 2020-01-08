FROM alpine:3.6

RUN apk add --no-cache git openssh-client gnupg

RUN mkdir -p /root/.ssh

ENTRYPOINT ["/usr/bin/git"]
