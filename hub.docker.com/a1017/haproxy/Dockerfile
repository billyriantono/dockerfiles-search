FROM alpine
ENV CONSUL_TEMPLATE_VERSION=0.10.0
RUN apk --update add haproxy wget
RUN wget --no-check-certificate \
    https://github.com/hashicorp/consul-template/releases/download/v${CONSUL_TEMPLATE_VERSION}/consul-template_${CONSUL_TEMPLATE_VERSION}_linux_amd64.tar.gz \
    -O /tmp/consul_template.tar.gz && gunzip /tmp/consul_template.tar.gz && \
    cd /tmp && tar xf /tmp/consul_template.tar && cd /tmp/consul-template* && \
    mv consul-template /usr/bin && rm -rf /tmp/*
COPY haproxy.json /tmp/haproxy.json
COPY haproxy.ctmpl /tmp/haproxy.ctmpl
EXPOSE 1936
ENTRYPOINT ["consul-template","-config=/tmp/haproxy.json"]
CMD ["-consul=consul.service.consul:8500"]
