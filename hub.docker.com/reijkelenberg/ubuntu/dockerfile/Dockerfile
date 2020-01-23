FROM alpine:3.5

LABEL caddy_version="0.10.4" architecture="amd64" caddy_plugins="tls.dns.route53"

COPY caddy /usr/bin/caddy
COPY Caddyfile /etc/Caddyfile

RUN apk --no-cache add ca-certificates

EXPOSE 80 443

VOLUME /root/.caddy

CMD ["/usr/bin/caddy", "--conf", "/etc/Caddyfile", "--log", "stdout"]
