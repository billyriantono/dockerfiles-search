FROM docker:1.12.5-dind
MAINTAINER Joshua Sierles <joshua@nextjournal.com>

ENV CONSUL_TEMPLATE_VERSION=0.16.0
ENV CONSUL_TEMPLATE_FILE=consul-template_${CONSUL_TEMPLATE_VERSION}_linux_amd64.zip
ENV CONSUL_TEMPLATE_URL="https://releases.hashicorp.com/consul-template/${CONSUL_TEMPLATE_VERSION}/${CONSUL_TEMPLATE_FILE}"

WORKDIR /tmp

RUN apk update && \
  apk add curl bash coreutils && \
  curl -sSLo $CONSUL_TEMPLATE_FILE $CONSUL_TEMPLATE_URL && \
  unzip $CONSUL_TEMPLATE_FILE && \
  mv consul-template /usr/local/bin/consul-template && \
  chmod a+x /usr/local/bin/consul-template && \
  apk del curl

RUN mkdir /rendered
VOLUME /rendered

ENTRYPOINT ["/usr/local/bin/consul-template"]
