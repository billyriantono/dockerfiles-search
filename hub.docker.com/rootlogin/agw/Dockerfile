# Build build-container
FROM node:8-alpine as builder

ARG GO_VERSION=1.10.2
ARG DEP_VERSION=0.4.1

ADD https://dl.google.com/go/go${GO_VERSION}.linux-amd64.tar.gz /tmp/golang.tar.gz

RUN set -ex \
    && apk -U --no-cache add \
        alpine-sdk \
        git \
        tar \
    && tar -C /usr/local -xzf /tmp/golang.tar.gz \
    && mkdir /lib64 \
    && ln -s /lib/libc.musl-x86_64.so.1 /lib64/ld-linux-x86-64.so.2 \
    && mkdir -p /opt/agw/src/github.com/chrootLogin/agw

ADD https://github.com/golang/dep/releases/download/v${DEP_VERSION}/dep-linux-amd64 /usr/local/go/bin/dep

COPY ./ /opt/agw/src/github.com/chrootLogin/agw

WORKDIR /opt/agw/src/github.com/chrootLogin/agw

RUN set -ex \
    && chmod +x /usr/local/go/bin/dep \
    && export PATH="${PATH}:/usr/local/go/bin:/usr/local/node-v${NODE_VERSION}-linux-x64/bin" \
    && export GOPATH="/opt/agw" \
    && go get -u github.com/nicksnyder/go-i18n/v2/goi18n \
    && go get -u github.com/jteeuwen/go-bindata/go-bindata \
    && sync \
    && GOOS=linux GOARCH=amd64 CGO_ENABLED=1 make

# Build agw container
FROM alpine:3.7

ARG BUILD_DATE
ARG VCS_REF

LABEL maintainer="Simon Erhardt <hello@rootlogin.ch>" \
  org.label-schema.name="AGW" \
  org.label-schema.description="Another wiki software written in Go." \
  org.label-schema.build-date=$BUILD_DATE \
  org.label-schema.vcs-ref=$VCS_REF \
  org.label-schema.vcs-url="https://github.com/chrootLogin/agw" \
  org.label-schema.schema-version="1.0"

RUN set -ex \
    && apk -U --no-cache add \
        tini

ENV DB_TYPE="sqlite" \
    DB_PATH="/db/data.sqlite" \
    GIN_MODE="release"

RUN mkdir -p /opt/agw

COPY docker-run.sh /
COPY --from=builder /opt/agw/src/github.com/chrootLogin/agw/agw /opt/agw/agw
COPY --from=builder /opt/agw/src/github.com/chrootLogin/agw/frontend/dist /opt/agw/frontend

EXPOSE 8080
VOLUME /db

ENTRYPOINT ["/sbin/tini","--"]
CMD ["/docker-run.sh"]
