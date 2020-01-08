FROM billyteves/alpine:3.5.0

MAINTAINER Benjamin Jones Teves <benjamin.stanley.jones@gmail.com>

ENV GOLANG_VERSION      1.9.2
ENV GOLANG_SRC_URL      https://golang.org/dl/go$GOLANG_VERSION.src.tar.gz
ENV GOLANG_SRC_SHA256   665f184bf8ac89986cfd5a4460736976f60b57df6b320ad71ad4cef53bb143dc
ENV GOPATH              /go
ENV PATH                $GOPATH/bin:/usr/local/go/bin:$PATH

# ssh for glide
COPY ./run-ssh /usr/local/bin/run-ssh

# https://golang.org/issue/14851
COPY ./patch-files/no-pic.patch /

RUN set -ex \
    && apk add --no-cache ca-certificates \
    && apk update --no-cache \
    && apk upgrade --no-cache \
    && apk add --no-cache --virtual .build-deps \

    # Install important apks for building go

    make \
    gcc \
    musl-dev \
    go \

    # Compile Golang 1.8 and cleanup

    && export GOROOT_BOOTSTRAP="$(go env GOROOT)" \
    && curl -L "$GOLANG_SRC_URL" > golang.tar.gz \
    && echo "$GOLANG_SRC_SHA256  golang.tar.gz" | sha256sum -c - \
    && tar -C /usr/local -xzf golang.tar.gz \
    && rm golang.tar.gz \
    && cd /usr/local/go/src \
    #&& patch -p2 -i /no-pic.patch \
    && ./make.bash \
    && rm -rf /*.patch \
    && apk del .build-deps \

    # Install needed apks

    && apk add --no-cache --virtual --update \
    git \
    make \
    glide \
    tzdata \

    # Make directories

    && mkdir -p $GOPATH/bin \
    && mkdir -p $GOPATH/src \

    # CHMOD

    && chmod -R 777 $GOPATH \
    && chmod +x /usr/local/bin/run-ssh \

    # Cleanup

    && rm -rf /var/cache/apk/* \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /tmp/*

WORKDIR /go/src/app
