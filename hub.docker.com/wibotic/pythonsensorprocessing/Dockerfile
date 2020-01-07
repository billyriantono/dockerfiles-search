# Designed for building on an x86 host
FROM alpine as qemubuild
RUN apk --no-cache add curl
RUN curl -L https://github.com/multiarch/qemu-user-static/releases/download/v3.1.0-2/qemu-arm-static.tar.gz | tar zxvf - -C /usr/bin && chmod +x /usr/bin/qemu-*

FROM arm32v6/python:3.7.2-alpine as pipbuild
COPY --from=qemubuild /usr/bin/qemu-* /usr/bin/

RUN \
  apk --no-cache add musl-dev g++ && \
  pip install --install-option="--prefix=/pipinstall" numpy

# Use a multi-stage build to not include build tools in image
FROM arm32v6/python:3.7.2-alpine
COPY --from=pipbuild /pipinstall /usr/local

