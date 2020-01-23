FROM golang:latest AS build

ARG DOCKER_LS_VERSION=v0.3.2
WORKDIR /go/src/github.com/mayflower/docker-ls
ENV CGO_ENABLED=0
ENV GOOS=linux
ENV GOARCH=amd64

RUN set -ex \
  && LC_ALL=C DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends ca-certificates \
  && curl -o docker-ls.tar.gz -SL https://github.com/mayflower/docker-ls/archive/${DOCKER_LS_VERSION}.tar.gz \
  && tar -xzf docker-ls.tar.gz --strip 1 -C /go/src/github.com/mayflower/docker-ls \
  && go build github.com/mayflower/docker-ls/cli/docker-ls \
  && go build github.com/mayflower/docker-ls/cli/docker-rm

FROM alpine:3.8
RUN set -ex\
  && apk add --no-cache ca-certificates bash bash-completion
COPY bashrc /root/.bashrc

LABEL MAINTAINER="code:Mayflower GmbH, Docker=https://github.com/timothyclarke/docker-ls"
COPY --from=build /go/src/github.com/mayflower/docker-ls/docker-* /bin/
