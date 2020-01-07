ARG GO_VERSION=1.13.0

FROM golang:${GO_VERSION}

LABEL maintainer="Steve Wallace <steve.wallace@blackironsoftware.com>"

RUN apt-get update && \
    apt-get -y --no-install-recommends install curl && \
    curl -sL https://deb.nodesource.com/setup_10.x | bash - && \
    apt-get -y --no-install-recommends install nodejs && \
    npm -g install serverless
