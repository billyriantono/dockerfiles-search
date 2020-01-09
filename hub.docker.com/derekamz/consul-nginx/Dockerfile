FROM derekamz/debian:slim

ENV CONSUL_TEMPLATE_VER 0.19.4

COPY build.sh /tmp
COPY entrypoint.sh /
COPY nginx.ctmpl /etc/nginx/

RUN chmod +x /tmp/build.sh && chmod +x /entrypoint.sh && /tmp/build.sh

# Create symlinks to redirect nginx logs to stdout and stderr docker log collector
# This only works if nginx is started with CMD or ENTRYPOINT
RUN ln -sf /dev/stdout /var/log/nginx/access.log
RUN ln -sf /dev/stderr /var/log/nginx/error.log

RUN cd /tmp \
    && curl https://releases.hashicorp.com/consul-template/${CONSUL_TEMPLATE_VER}/consul-template_${CONSUL_TEMPLATE_VER}_linux_amd64.tgz -o consul-template_${CONSUL_TEMPLATE_VER}_linux_amd64.tgz \
    && tar xzvf consul-template_${CONSUL_TEMPLATE_VER}_linux_amd64.tgz -C /usr/bin/ \
    && chmod +x /usr/bin/consul-template

EXPOSE 80 443

EXPOSE 3000-9000

ENTRYPOINT [ "/entrypoint.sh" ]
CMD ["nginx", "-g", "daemon off;"]