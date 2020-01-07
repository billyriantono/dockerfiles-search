FROM golang 

MAINTAINER Tamas VARGA <tamas@alapzaj.com>

ARG VERSION=2.3.0
ARG TARGETOS=linux
ARG TARGETARCH=amd64
EXPOSE 179

WORKDIR /go

RUN wget https://github.com/osrg/gobgp/releases/download/v${VERSION}/gobgp_${VERSION}_${TARGETOS}_${TARGETARCH}.tar.gz && tar xvzf gobgp_${VERSION}_${TARGETOS}_${TARGETARCH}.tar.gz && rm -rf gobgp_${VERSION}_${TARGETOS}_${TARGETARCH}.tar.gz

RUN mkdir /etc/gpbgp

COPY gobgp.conf /etc/gobgp/gobgp.conf

WORKDIR /go

CMD /go/gobgpd -f /etc/gobgp/gobgp.conf -p
