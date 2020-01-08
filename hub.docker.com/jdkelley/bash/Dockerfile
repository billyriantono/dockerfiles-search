#
# docker run --rm \
#     -it \
#     jdkelley/bash
#
ARG ALPINE_VERSION=3.10
FROM jdkelley/alpine:${ALPINE_VERSION}

LABEL maintainer="jdkelley.oss@gmail.com"

WORKDIR /scripts

RUN apk --no-cache add bash 

ENTRYPOINT [ "/bin/bash" ]
