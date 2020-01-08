FROM golang:1-alpine3.8

LABEL maintainer="frank.giesecke@final-gene.de"

ENV GITHUB_RELEASE_VERSION "v0.7.2"

RUN apk add --no-cache --virtual=.build-deps \
        bash=4.4.19-r1 \
        curl=7.61.1-r0

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

RUN apk add --no-cache \
        git=2.18.0-r0

RUN curl -sSL https://github.com/aktau/github-release/releases/download/${GITHUB_RELEASE_VERSION}/linux-amd64-github-release.tar.bz2 \
        | tar -xjf - -C /tmp \
    && mv /tmp/bin/linux/amd64/github-release /usr/local/bin \
    && rm -rf /tmp/

RUN apk del .build-deps

COPY docker-entrypoint.sh /usr/local/bin/docker-entrypoint.sh

WORKDIR /app

ENTRYPOINT ["/usr/local/bin/docker-entrypoint.sh"]

CMD [""]
