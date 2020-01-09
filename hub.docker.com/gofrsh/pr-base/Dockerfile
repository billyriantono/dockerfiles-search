FROM koalaman/shellcheck-alpine

COPY askpass.sh github.sh /opt/

RUN set -x \
    && shellcheck /opt/*.sh

FROM golang:1.10-alpine3.7

RUN apk add --no-cache \
    git \
    bash \
    jq \
    openssh \
    curl

RUN set -x \
    && git version \
    && go version

COPY askpass.sh github.sh /opt/

