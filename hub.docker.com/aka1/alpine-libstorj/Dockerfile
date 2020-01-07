FROM alpine:3.8 AS builder

LABEL maintainer="Ammar K." \
      stage=intermediate

ARG VERSION=tags/v2.0.0-beta2
ARG REPOSITORY=storj/libstorj
ARG BUILDER_URL=https://raw.githubusercontent.com/akai-z/libstorj-alpine-source-builder/master/libstorj-alpine-source-builder.sh

ADD $BUILDER_URL /usr/local/bin

RUN set -x \
    && chmod +x /usr/local/bin/libstorj-alpine-source-builder.sh \
    && libstorj-alpine-source-builder.sh \
        -build_deps_install \
        --repository="$REPOSITORY" \
        --version="$VERSION" \
    && libstorj-alpine-source-builder.sh \
        -build_deps_delete \
        clean

FROM alpine:3.8

LABEL maintainer="Ammar K."

COPY --from=builder /usr/local/bin/storj \
    /usr/local/bin/libstorj-alpine-source-builder.sh \
    /usr/local/bin/

RUN set -x \
    && libstorj-alpine-source-builder.sh \
        run_deps_install \
    && rm -f /usr/local/bin/libstorj-alpine-source-builder.sh
