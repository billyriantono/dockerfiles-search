FROM haproxy:1.8.13-alpine
RUN touch /var/log/haproxy.log \
    && ln -sf /dev/stdout /var/log/haproxy.log \
    && mkdir /run/haproxy
RUN adduser -D -u 1000 haproxy \
    && chown haproxy:haproxy /run/haproxy
