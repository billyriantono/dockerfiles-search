FROM haproxy:alpine
ENV CONSUL_TEMPLATE_VER 0.19.4

RUN apk update && apk add curl \
    && cd /tmp \
    && curl https://releases.hashicorp.com/consul-template/${CONSUL_TEMPLATE_VER}/consul-template_${CONSUL_TEMPLATE_VER}_linux_amd64.tgz -o consul-template_${CONSUL_TEMPLATE_VER}_linux_amd64.tgz \
    && tar xzvf consul-template_${CONSUL_TEMPLATE_VER}_linux_amd64.tgz -C /usr/bin/ \
    && chmod +x /usr/bin/consul-template
COPY entrypoint.sh /
COPY config.hcl /config.hcl
COPY haproxy.ctmpl /haproxy.ctmpl
COPY reload.sh /reload.sh

ENTRYPOINT [ "/entrypoint.sh" ]
CMD ["haproxy", "-f", "/usr/local/etc/haproxy/haproxy.cfg"]