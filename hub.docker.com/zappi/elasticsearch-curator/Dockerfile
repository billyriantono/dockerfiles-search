FROM alpine:3.10.3

LABEL maintainer "Zappi DevOps <devops@zappistore.com>"

ARG APP_DEPS="python py-setuptools"
ARG BUILD_DEPS="py-pip"
ARG CURATOR_VERSION="5.8.1"

RUN apk --update add ${APP_DEPS} ${BUILD_DEPS} && \
    pip install elasticsearch-curator==${CURATOR_VERSION} && \
    apk del ${BUILD_DEPS} && \
    rm -rf /var/cache/apk/*

USER nobody:nobody
ENTRYPOINT ["/usr/bin/curator"]
