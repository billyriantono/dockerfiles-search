FROM docker:18.05.0-ce-git

ENV GOLANG_VERSION 1.10.2

RUN apk add --no-cache --virtual .build-deps \
            bash \
    		ca-certificates \
    		gcc \
    		go \
    		groff \
    		less \
            musl-dev \
            openssl \
            py-pip \
    	; \
    	export \
        # set GOROOT_BOOTSTRAP such that we can actually build Go
        		GOROOT_BOOTSTRAP="$(go env GOROOT)" \
        # ... and set "cross-building" related vars to the installed system's values so that we create a build targeting the proper arch
        # (for example, if our build host is GOARCH=amd64, but our build env/image is GOARCH=386, our build needs GOARCH=386)
        		GOOS="$(go env GOOS)" \
        		GOARCH="$(go env GOARCH)" \
        		GO386="$(go env GO386)" \
        		GOARM="$(go env GOARM)" \
        		GOHOSTOS="$(go env GOHOSTOS)" \
        		GOHOSTARCH="$(go env GOHOSTARCH)" \
        	; \
    	wget -O go.tgz "https://golang.org/dl/go$GOLANG_VERSION.src.tar.gz"; \
    	echo '665f184bf8ac89986cfd5a4460736976f60b57df6b320ad71ad4cef53bb143dc *go.tgz' | sha256sum -c -; \
    	tar -C /usr/local -xzf go.tgz; \
    	rm go.tgz; \
    	\
        	cd /usr/local/go/src; \
        	for p in /go-alpine-patches/*.patch; do \
        		[ -f "$p" ] || continue; \
        		patch -p2 -i "$p"; \
        	done; \
        	./make.bash; \
        	\
        	rm -rf /go-alpine-patches; \
        	pip install awscli; \
        	apk del .build-deps py-pip ; \
        	apk add --no-cache python ca-certificates openssl gettext;  \
        	\
        	export PATH="/usr/local/go/bin:$PATH"; \
        	go version

ENV GOPATH /go
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH

RUN mkdir -p "$GOPATH/src" "$GOPATH/bin" && chmod -R 777 "$GOPATH"
WORKDIR $GOPATH