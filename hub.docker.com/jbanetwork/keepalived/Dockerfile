FROM alpine:3.3

ENV CONSUL_TEMPLATE_VERSION 0.14.0

RUN echo "@testing http://nl.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories && \
	apk add --update --no-cache wget unzip bash iproute2 keepalived@testing ipvsadm@testing && \
    wget --no-check-certificate https://releases.hashicorp.com/consul-template/${CONSUL_TEMPLATE_VERSION}/consul-template_${CONSUL_TEMPLATE_VERSION}_linux_amd64.zip -O /tmp/consul-template.zip && \
    unzip /tmp/consul-template.zip -d /usr/local/bin && \
    rm -rf /tmp/consul-template.zip

COPY setup.sh /root/setup.sh
COPY restart_keepalived.sh /root/restart_keepalived.sh
COPY keepalived.conf.tmpl /root/keepalived.conf.tmpl

WORKDIR /root

CMD /bin/sh setup.sh
