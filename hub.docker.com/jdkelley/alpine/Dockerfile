ARG ALPINE_VERSION=3.10
FROM alpine:${ALPINE_VERSION} as alpine-base

RUN apk upgrade --no-cache -U -a

FROM scratch 
LABEL maintainer="jdkelley.oss@gmail.com"

COPY --from=alpine-base / /
