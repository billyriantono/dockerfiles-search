FROM gliderlabs/alpine:3.1
MAINTAINER Hendrik Volkmer <hvolkmer@gmail.com>
ENV CONSUL_TEMPLATE_VERSION=0.10.0

ADD https://github.com/hashicorp/consul-template/releases/download/v${CONSUL_TEMPLATE_VERSION}/consul-template_${CONSUL_TEMPLATE_VERSION}_linux_amd64.tar.gz /tmp/consul-template.tar.gz
RUN cd /tmp && tar -xvzf /tmp/consul-template.tar.gz && mv /tmp/consul-template_0.10.0_linux_amd64/consul-template /bin/consul-template && chmod +x /bin/consul-template && rm -rf /tmp/consul-template*

RUN mkdir -p /etc/nginx/external
RUN mkdir /templates
ADD templates/* /templates/

ENTRYPOINT ["/bin/consul-template","-config", "/templates/consul-template-config.hcl"]

