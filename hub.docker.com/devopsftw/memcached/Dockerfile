FROM memcached:1.4-alpine
MAINTAINER Alex Salt <holy.cheater@gmail.com>

ENV CONSUL_VERSION 0.7.0

USER root

RUN apk add --no-cache ca-certificates openssl && \
    wget https://releases.hashicorp.com/consul/${CONSUL_VERSION}/consul_${CONSUL_VERSION}_linux_amd64.zip && \
    unzip -d /usr/local/bin consul_${CONSUL_VERSION}_linux_amd64.zip && \
    wget https://github.com/kreuzwerker/envplate/releases/download/v0.0.8/ep-linux -O /usr/local/bin/ep && \
    chmod +x /usr/local/bin/ep && \
    apk del openssl

COPY entry-consul.sh /bin
COPY consul.tpl.json /etc

ENTRYPOINT [ "entry-consul.sh" ]
CMD [ "memcached" ]
