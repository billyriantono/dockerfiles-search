# Usage:
# docker run --rm -it \
# -v /:/host
# yrcjaya/rmlint \
# /host

FROM alpine:latest
LABEL maintainer "Jayaseelan Yezhuaralai <yrcjaya@gmail.com>"

RUN apk add --no-cache \
        build-base \
        ca-certificates \
        python2 \
        python3 \
        glib-dev \
        libelf-dev \
        scons \
        gettext \
        git

RUN set -xu \
        && git clone --depth 1 https://github.com/sahib/rmlint.git \
        && cd rmlint \
        && scons config \
        && scons DEBUG=1 --prefix=/usr install

WORKDIR /host
ENTRYPOINT ["/usr/bin/rmlint"]
CMD ["rmlint", "--help"]
