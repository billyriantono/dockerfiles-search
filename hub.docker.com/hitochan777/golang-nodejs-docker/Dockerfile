FROM node:9.3.0

MAINTAINER hitochan777@gmail.com

ENV GOLANG_VERSION 1.9.2

RUN set -eux; \
    wget -O go.tgz "https://dl.google.com/go/go$GOLANG_VERSION.linux-amd64.tar.gz"; \
         tar -C /usr/local -xzf go.tgz; \
         rm go.tgz; \
         export PATH="/usr/local/go/bin:$PATH"; 

ENV GOPATH /go
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH

RUN mkdir -p "$GOPATH/src" "$GOPATH/bin" && chmod -R 777 "$GOPATH"
WORKDIR $GOPATH

CMD ["go", "version"]

