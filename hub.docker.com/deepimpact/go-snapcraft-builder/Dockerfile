FROM snapcore/snapcraft

ENV PATH=$PATH:/usr/local/go/bin \
    GOPATH=/go \
    GOVERSION=1.10.3 \
    GORELEASERVERSION=v0.79.0

RUN   apt-get update \
   && apt-get install -y wget curl zip \
   && mkdir /go \
   && GOARCHIVE=go${GOVERSION}.linux-amd64.tar.gz \
   && wget https://dl.google.com/go/${GOARCHIVE} \
   && tar -C /usr/local -xzf ${GOARCHIVE} \
   && rm -f ${GOARCHIVE} \
   && GORELEASERARCHIVE=goreleaser_Linux_x86_64.tar.gz \
   && wget https://github.com/goreleaser/goreleaser/releases/download/${GORELEASERVERSION}/${GORELEASERARCHIVE} \
   && tar -C /tmp -xf ${GORELEASERARCHIVE} \
   && mv /tmp/goreleaser /usr/local/bin \
   && rm -f ${GORELEASERARCHIVE} \
   && apt-get remove -y curl wget \
   && apt-get autoremove -y \
   && rm -rf /var/lib/apt/lists/* \
   && rm -fr /tmp/*
