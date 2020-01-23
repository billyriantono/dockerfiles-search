FROM alpine:3.7

ENV GOLANG_DOWNLOAD_URL=https://golang.org/dl/go1.9.2.linux-amd64.tar.gz \
    GOLANG_DOWNLOAD_SHA256=de874549d9a8d8d8062be05808509c09a88a248e77ec14eb77453530829ac02b \
    GOPATH=/go \
    LOCAL_NPM_MIRROR=https://registry.npm.taobao.org \
    LOCAL_NPM_DISTURL_MIRROR=https://npm.taobao.org/dist \
    GRAFANA_VERSION=4.6.3 \
    GRAFANA_DOWNLOAD_URL=https://github.com/grafana/grafana/archive/v4.6.3.tar.gz

RUN mkdir /build && \
    adduser -u 990 -g 990 -D -s /bin/sh -h /openmetric openmetric && \
    apk add --no-cache --virtual .build-deps su-exec libc6-compat curl ca-certificates netcat-openbsd git mercurial make nodejs gcc g++ && \
    mkdir -p /openmetric/conf /openmetric/log /openmetric/data && \
    chown openmetric:openmetric -R /openmetric/ && \
    npm config set cache /build/.npm/ && \
    npm config set registry ${LOCAL_NPM_MIRROR} && \
    npm config set disturl ${LOCAL_NPM_DISTURL_MIRROR} && \
    npm install -g yarn && \
    yarn config set registry ${LOCAL_NPM_MIRROR} && \
    curl -fsSL ${GOLANG_DOWNLOAD_URL} -o /build/golang.tar.gz && \
    echo "$GOLANG_DOWNLOAD_SHA256  /build/golang.tar.gz" | sha256sum -c - && \
    tar -C /usr/local -zxf /build/golang.tar.gz && \
    mkdir -p "${GOPATH}/src" "${GOPATH}/bin" && \
    export GOPATH=/go && \
    export PATH=${GOPATH}/bin:/usr/local/go/bin:$PATH && \
    mkdir -p ${GOPATH}/src/github.com/grafana/grafana && \
    mkdir /build/tmp && \
    curl -fsSL ${GRAFANA_DOWNLOAD_URL} -o /build/grafana.tar.gz && \
    tar -C /build/tmp -zxf /build/grafana.tar.gz && \
    mv /build/tmp/grafana-${GRAFANA_VERSION}/* ${GOPATH}/src/github.com/grafana/grafana && \
    cd ${GOPATH}/src/github.com/grafana/grafana && \
    go run build.go setup && \
    go run build.go build && \
    yarn install --pure-lockfile && \
    ./node_modules/.bin/grunt release && \
    install -v -D -m 755 /go/src/github.com/grafana/grafana/tmp/bin/grafana-server /usr/bin/grafana-server && \
    install -v -D -m 755 /go/src/github.com/grafana/grafana/tmp/bin/grafana-cli /usr/bin/grafana-cli && \
    install -v -d -m 755 /usr/share/grafana && \
    cp -r /go/src/github.com/grafana/grafana/tmp/public /usr/share/grafana/public && \
    cp -r /go/src/github.com/grafana/grafana/tmp/conf /usr/share/grafana/conf && \
    find /usr/share/grafana/ -name '*.js.map' -delete && \
    npm uninstall -g yarn && \
    npm cache clear && \
    apk del --purge .build-deps && \
    rm -rf /var/cache/apk/* && \
    rm -rf /usr/local/go /go && \
    find /usr/lib/python2.7/ -name '*.py[co]' -delete || true && \
    find /usr/lib/python2.7/ -name 'test_*.py' -delete || true && \
    find /usr/lib/python2.7/ -name 'test_*.py[co]' -delete || true && \
    rm -rf /build && \
    find /root -mindepth 1 -maxdepth 1 -exec rm -rf {} \; && \
    rm -rf /tmp/* && \
    rm -rf /usr/lib/node_modules/

VOLUME ["/openmetric/conf", "/openmetric/log", "/openmetric/data"]

EXPOSE 3000