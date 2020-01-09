FROM golang:1.13-alpine

ARG BUILD_DATE
ARG VCS_REF

ENV COMPOSER_ALLOW_SUPERUSER 1

LABEL Maintainer="Tobias Sjösten <tobias.sjosten@stim.se>" \
      Description="Go 1.13 image with batteries included" \
      org.label-schema.name="stimtech/builder-go" \
      org.label-schema.description="Go 1.13 image with batteries included" \
      org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.vcs-url="https://bitbucket.org/stimtech/docker-builder-go" \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.schema-version="1.0.0"

SHELL ["/bin/ash", "-eo", "pipefail", "-c"]
RUN set -ex \
    && apk update \
    && apk add --no-cache g++=8.3.0-r0 gcc=8.3.0-r0 git=2.22.0-r0 \
    && wget -O - -q https://install.goreleaser.com/github.com/golangci/golangci-lint.sh | sh -s v1.19.1 \
    && go get github.com/schrej/godacov \
    && rm -rf /tmp/*
