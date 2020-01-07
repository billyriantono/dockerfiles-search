FROM alpine:3.3

ENV CONSUL_VERSION=0.6.2
ENV CONSUL_FILENAME=consul_${CONSUL_VERSION}_linux_amd64.zip
ENV CONSUL_URL=https://releases.hashicorp.com/consul/${CONSUL_VERSION}/${CONSUL_FILENAME}
ENV CONSUL_CHECKSUM_URL=https://releases.hashicorp.com/consul/${CONSUL_VERSION}/consul_${CONSUL_VERSION}_SHA256SUMS

WORKDIR /tmp

RUN apk add --no-cache wget ca-certificates && \
    update-ca-certificates && \
    wget $CONSUL_URL && \
    wget -qO- ${CONSUL_CHECKSUM_URL} | grep ${CONSUL_FILENAME} > consul_checksum &&\
    sha256sum -c consul_checksum && \
    unzip $CONSUL_FILENAME -d /usr/local/bin && \
    rm consul_checksum ${CONSUL_FILENAME}

ADD ./config /etc/consul/server

EXPOSE 8300 8301 8500/tcp 53/udp

VOLUME /var/lib/consul

ENTRYPOINT [ "/usr/local/bin/consul", "agent", "-config-dir=/etc/consul/server" ]
