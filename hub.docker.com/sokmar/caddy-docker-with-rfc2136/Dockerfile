FROM abiosoft/caddy:builder AS builder

ARG version="0.10.11"

RUN VERSION=${version} PLUGINS="rfc2136" /bin/sh /usr/bin/builder.sh

FROM alpine:3.7
LABEL maintainer "Marcin Pertek <marcin@sokrates.com.pl>"

COPY --from=builder /install/caddy /usr/bin/caddy

RUN /usr/bin/caddy -version
RUN /usr/bin/caddy -plugins

EXPOSE 80 443 2015
VOLUME /root/.caddy /srv
WORKDIR /srv

COPY Caddyfile /etc/Caddyfile

ENTRYPOINT ["/usr/bin/caddy"]
CMD ["--conf", "/etc/Caddyfile", "--log", "stdout"]

