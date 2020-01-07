FROM gocd/gocd-agent-alpine-3.9:v19.5.0

RUN \
	apk --no-cache update \
    apk --no-cache upgrade \
    && apk add --no-cache git ca-certificates

ENV GOLANG_VERSION 1.12.5
ENV GOLANG_SHA256SUM 2aa5f088cbb332e73fc3def546800616b38d3bfe6b8713b8a6404060f22503e8
ENV GOOS linux
ENV GOARCH amd64
ENV GOHOSTOS linux
ENV GOHOSTARCH amd64

RUN set -eux; \
	apk add --no-cache --virtual .build-deps bash gcc musl-dev openssl go

RUN set -eux; \
	export \
# set GOROOT_BOOTSTRAP such that we can actually build Go
		GOROOT_BOOTSTRAP="$(go env GOROOT)" \
# ... and set "cross-building" related vars to the installed system's values so that we create a build targeting the proper arch
# (for example, if our build host is GOARCH=amd64, but our build env/image is GOARCH=386, our build needs GOARCH=386)
		GOOS="$(go env GOOS)" \
		GOARCH="$(go env GOARCH)" \
		GOHOSTOS="$(go env GOHOSTOS)" \
		GOHOSTARCH="$(go env GOHOSTARCH)" \
	; \
# also explicitly set GO386 and GOARM if appropriate
# https://github.com/docker-library/golang/issues/184
	apkArch="$(apk --print-arch)"; \
	case "$apkArch" in \
		armhf) export GOARM='6' ;; \
		x86) export GO386='387' ;; \
	esac; \
	\
	wget -O go.tgz "https://golang.org/dl/go$GOLANG_VERSION.src.tar.gz"; \
	echo "$GOLANG_SHA256SUM *go.tgz" | sha256sum -c -; \
	tar -C /usr/local -xzf go.tgz; \
	rm go.tgz; \
	\
	cd /usr/local/go/src; \
	./make.bash; \
	\
# https://github.com/golang/go/blob/0b30cf534a03618162d3015c8705dd2231e34703/src/cmd/dist/buildtool.go#L121-L125
# https://golang.org/cl/82095
# https://github.com/golang/build/blob/e3fe1605c30f6a3fd136b561569933312ede8782/cmd/release/releaselet.go#L56
	rm -rf /usr/local/go/pkg/bootstrap /usr/local/go/pkg/obj; \
	apk del .build-deps go musl-dev;

RUN ln -s /usr/local/go/bin/go /usr/local/go/bin/gofmt /usr/local/go/bin/godoc /usr/local/bin/; \
	go version; \
	go env;
