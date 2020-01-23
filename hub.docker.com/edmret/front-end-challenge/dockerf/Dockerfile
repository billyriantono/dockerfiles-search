FROM alpine:3.5

RUN apk --update add --no-cache wget ca-certificates python py-setuptools py-pip && \
    pip install elasticsearch-curator==5.5.4 && \
	apk del py-pip

# Install consul-template
ENV CONSUL_TEMPLATE_VERSION 0.19.5
ENV CONSUL_TEMPLATE_SHA256 39f4fc2ffaa00e0a7504f531f922d9d39dd29520c03dc0abde46835ebd52c647

RUN wget -q -O /tmp/consul-template.tgz https://releases.hashicorp.com/consul-template/${CONSUL_TEMPLATE_VERSION}/consul-template_${CONSUL_TEMPLATE_VERSION}_linux_amd64.tgz \
    && echo `sha256sum /tmp/consul-template.tgz` \
    && echo "${CONSUL_TEMPLATE_SHA256} /tmp/consul-template.tgz" \
    && echo "${CONSUL_TEMPLATE_SHA256}  /tmp/consul-template.tgz" | sha256sum -c - \
    && tar zxf /tmp/consul-template.tgz -C /usr/local/bin \
    && chmod +x /usr/local/bin/consul-template \
    && rm /tmp/consul-template.tgz

COPY docker-entrypoint.sh /docker-entrypoint.sh
COPY run.sh /run.sh

ENTRYPOINT ["/docker-entrypoint.sh"]

CMD ["/run.sh"]
