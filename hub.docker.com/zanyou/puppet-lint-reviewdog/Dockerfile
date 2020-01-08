FROM alpine:3.8

RUN apk update && \
apk upgrade && \
apk add --no-cache ca-certificates wget bash git openssh ruby ruby-bundler ruby-dev ruby-json && \
update-ca-certificates

RUN gem install puppet-lint --no-document

RUN mkdir /lib64 && ln -s /lib/libc.musl-x86_64.so.1 /lib64/ld-linux-x86-64.so.2

ENV REVIEWDOG_VERSION 0.9.11

RUN wget -O /usr/local/bin/reviewdog -q https://github.com/haya14busa/reviewdog/releases/download/$REVIEWDOG_VERSION/reviewdog_linux_amd64 && \
chmod +x /usr/local/bin/reviewdog
