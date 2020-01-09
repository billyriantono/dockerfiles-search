FROM haproxy:1.6

MAINTAINER Michal Tomczuk <michal.tomczuk@zerodowntime.pl>

RUN apt-get update && apt-get install -y zip unzip --no-install-recommends && rm -rf /var/lib/apt/lists/*

ENV CONSUL_TEMPLATE_VERSION=0.15.0

ADD https://releases.hashicorp.com/consul-template/${CONSUL_TEMPLATE_VERSION}/consul-template_${CONSUL_TEMPLATE_VERSION}_linux_amd64.zip /

RUN unzip /consul-template_${CONSUL_TEMPLATE_VERSION}_linux_amd64.zip  && \
    mv /consul-template /usr/local/bin/consul-template && \
    rm -rf /consul-template_${CONSUL_TEMPLATE_VERSION}_linux_amd64.zip

COPY templates/haproxy.json /consul-template/template.d/haproxy.json
COPY templates/haproxy.ctmpl /consul-template/template.d/haproxy.ctmpl

CMD ["consul-template", "-consul=consul.service.consul:8500", "-config=/consul-template/template.d/haproxy.json"]
