FROM alpine:3.3

ENV PACKAGES "git openssh-client gnupg bash"

RUN apk add --update $PACKAGES && rm -rf /var/cache/apk/*

RUN mkdir -p /root/.ssh

RUN git config --global user.email "wuchuansheng@yeah.net" && \
    git config --global user.name "goddy"