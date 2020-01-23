FROM alpine:3.4

RUN apk add --update --no-cache openssh-client tar curl

RUN curl --silent --show-error --fail --location \
    "https://caddyserver.com/download/build?os=linux&arch=amd64&features=ipfilter" \
    | tar --no-same-owner -C /usr/local/bin/ -xz caddy \
    && chmod 0755 /usr/local/bin/caddy

EXPOSE 80 443
WORKDIR /caddy
VOLUME /caddy

ENV CADDYPATH /home/caddy
VOLUME /home/caddy

ENTRYPOINT ["/usr/local/bin/caddy"]/
CMD ["--conf=/caddy/Caddyfile", "--http2=false"]
