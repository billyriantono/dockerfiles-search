FROM golang:alpine as builder

ARG CONFD_VER=0.21.0

WORKDIR /go/src/github.com/szyhf
RUN wget -q https://github.com/szyhf/go-nacos-confd/archive/v${CONFD_VER}.tar.gz \
    && tar -xf v${CONFD_VER}.tar.gz \
	&& rm -rf v${CONFD_VER}.tar.gz \
	&& mv go-nacos-confd-${CONFD_VER} go-nacos-confd \
	&& cd go-nacos-confd \
	&& go build -o nacos-confd

FROM szyhf/alpine-glibc:latest

COPY --from=0 /go/src/github.com/szyhf/go-nacos-confd/nacos-confd /

RUN chmod u+x /nacos-confd \
	&& mkdir -p /etc/confd/conf.d \
	&& mkdir -p /etc/confd/templates

# confd -watch -backend nacos -endpoint ${ACM_ENDPOINT}:8080 -namespace ${ACM_NAMESPACE} -group ${ACM_GROUP} -accessKey ${ACM_AK} -secretKey ${ACM_SK} -openKMS true/false -regionId kmsRegionID
ENTRYPOINT [ "/nacos-confd" ]