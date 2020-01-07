FROM alpine:latest
MAINTAINER Wojciech Urbański

ENV GIT_COMMITTER_NAME  Autobuild
ENV GIT_COMMITTER_EMAIL build@buildhost.local
ENV GIT_AUTHOR_NAME     Autobuild
ENV GIT_AUTHOR_EMAIL    build@buildhost.local

RUN apk add --no-cache git openssh-client ca-certificates && mkdir ~/.ssh && touch ~/.ssh/known_hosts
