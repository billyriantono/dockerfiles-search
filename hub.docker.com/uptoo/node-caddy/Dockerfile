FROM node:10

ARG version="0.10.10"
ARG plugins="http.git"

LABEL maintainer="Uptoo <docker@uptoo.fr>"

RUN curl -fsSL "https://caddyserver.com/download/linux/amd64?plugins=${plugins}&license=personal" -o caddy.tar.gz \
    && $(mkdir caddy && cd caddy && tar -xzf ../caddy.tar.gz && mv caddy /usr/bin) \
    && rm -rf caddy.tar.gz caddy

WORKDIR /srv

ENTRYPOINT ["/usr/bin/caddy"]
CMD ["--conf", "/etc/Caddyfile", "--log", "stdout"]