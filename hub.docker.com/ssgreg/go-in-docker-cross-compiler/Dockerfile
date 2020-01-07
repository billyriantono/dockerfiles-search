FROM ssgreg/go-in-docker-cross-compiler:base-latest
LABEL maintainer="me@ssgreg.com"

ENV VERSION 1.9.2
ENV FILE go$VERSION.linux-amd64.tar.gz
ENV URL https://storage.googleapis.com/golang/$FILE
ENV SHA256 de874549d9a8d8d8062be05808509c09a88a248e77ec14eb77453530829ac02b

ENV GOPATH /go
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH

RUN set -ex ; \
    curl -OL $URL ; \
        echo "$SHA256  $FILE" | sha256sum -c - ; \
        tar -C /usr/local -xzf $FILE ; \
        rm $FILE ; \
    mkdir -p "$GOPATH/src" "$GOPATH/bin"

WORKDIR $GOPATH
