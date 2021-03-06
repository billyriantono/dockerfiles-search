#+++++++++++++++++++++++++++++++++++++++#
#   Golang Docker container in Alpine   #
#+++++++++++++++++++++++++++++++++++++++#


FROM alpine
LABEL vendor=Featx
MAINTAINER Excepts <excepts@aliyun.com>

ENV GOLANG_VERSION=1.11.5 \
    GOSU_VERSION=1.11 \
    GOPATH=/usr/local \
    PATH=/usr/local/go/bin:$PATH

RUN set -ex \
  # User create
  && addgroup -g 1000 feat && adduser -G feat -u 1000 -s /sbin/nologin -D -H feat \
  # Fixed dep
  && apk add --no-cache ca-certificates \
  # Build dep
  && apk add --no-cache --virtual .build-deps \
    bash gcc musl-dev go openssl gnupg \
  # Build env
  && export GOROOT_BOOTSTRAP="$(go env GOROOT)" \
    GOOS="$(go env GOOS)" \
    GOARCH="$(go env GOARCH)" \
    GOHOSTOS="$(go env GOHOSTOS)" \
    GOHOSTARCH="$(go env GOHOSTARCH)" \
    apkArch="$(apk --print-arch)" \
  && case "$apkArch" in \
        armhf) export GOARM='6' ;; \
        x86) export GO386='387' ;; \
    esac \
  # Download src bundle and veryfied, unzip, delete .zip	
  && wget -O go.tgz "https://golang.org/dl/go$GOLANG_VERSION.src.tar.gz" \
  && echo 'bc1ef02bb1668835db1390a2e478dcbccb5dd16911691af9d75184bbe5aa943e *go.tgz' | sha256sum -c - \
  && tar -C /usr/local -xzf go.tgz \
  && rm go.tgz \
  # Go to src to build 
  && cd /usr/local/go/src \
  && ./make.bash \
  # Grab gosu for easy step-down from root
  && wget -O /usr/local/bin/gosu "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-amd64" \
  && wget -O /usr/local/bin/gosu.asc "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-amd64.asc" \
  && export GNUPGHOME="$(mktemp -d)" \
  && gpg --keyserver pgp.mit.edu --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4 \
  && gpg --batch --verify /usr/local/bin/gosu.asc /usr/local/bin/gosu \
  && chmod +x /usr/local/bin/gosu \
  && gosu nobody true \
  && echo 'hosts: files mdns4_minimal [NOTFOUND=return] dns mdns4' >> /etc/nsswitch.conf \
  #[ ! -e /etc/nsswitch.conf ] && echo 'hosts: files dns' > /etc/nsswitch.conf
  # Dispose 
  && apk del .build-deps \
  && rm -rf /var/cache/apk/* "$GNUPGHOME" /usr/local/bin/gosu.asc \
    /usr/local/go/pkg/bootstrap /usr/local/go/pkg/obj \
    /usr/local/go/doc /usr/local/go/api /usr/local/go/test

CMD ["go", "version"]