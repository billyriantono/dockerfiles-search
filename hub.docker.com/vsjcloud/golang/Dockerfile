FROM vsjcloud/dep-common:0.1
LABEL maintainer="tech@vsj.vn"

ENV GOLANG_VERSION 1.12.8

RUN goRelArch='linux-amd64'; \
        goRelSha256='bd26cd4962a362ed3c11835bca32c2e131c2ae050304f2c4df9fa6ded8db85d2'; \
        url="https://dl.google.com/go/go${GOLANG_VERSION}.${goRelArch}.tar.gz"; \
        wget -O go.tgz "$url"; \
        echo "${goRelSha256} *go.tgz" | sha256sum -c -; \
        tar -C /usr/local -xzf go.tgz; \
	    rm go.tgz; \
        export PATH="/usr/local/go/bin:$PATH"; \
        go version

ENV GOPATH /go
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH

RUN mkdir -p "$GOPATH/src" "$GOPATH/bin" && chmod -R 777 "$GOPATH"
WORKDIR $GOPATH
