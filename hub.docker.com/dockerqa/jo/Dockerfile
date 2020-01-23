FROM alpine:3.4
MAINTAINER qa@docker.com

ENV BUILD_PACKAGES build-base git autoconf automake
ENTRYPOINT ["jo"]

RUN apk update && \
    apk upgrade && \
    apk add $BUILD_PACKAGES && \
    git clone https://github.com/jpmens/jo.git -b v1.0 jo && \
    cd jo && \
    autoreconf -i && \
    ./configure && \
    make check && \
    make install && \
    cd .. && \
    apk del $BUILD_PACKAGES && \
    rm -rf jo /var/cache/apk/* && \
    jo -v
